---
title: "Que sont les notifications d'intégrité de service | Microsoft Docs"
description: "Les notifications d’intégrité de service vous permettent d’afficher les messages d’intégrité de service publiés par Microsoft Azure."
author: anirudhcavale
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: d85281c02b792921f12cc62e6d60bef3e7c13b3f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="service-health-notifications"></a>Notifications d'intégrité de service
## <a name="overview"></a>Vue d'ensemble

Cet article vous montre comment afficher des notifications d'intégrité de service avec le Portail Azure.

Les notifications d’intégrité de service vous permettent d’afficher les messages d’intégrité de service publiés par l’équipe Azure susceptibles d’affecter les ressources de votre abonnement. Ces notifications sont une sous-classe des événements du journal d’activité et figurent également dans le panneau Journal d’activité. Les notifications d’intégrité de service peuvent être informatives ou exploitables en fonction de la classe.

Il existe cinq classes de notifications de contrôle d’intégrité :  

- **Action requise :** De temps à autre, nous pouvons remarquer quelque chose d’inhabituel sur votre compte. Nous pourrions avoir à travailler avec vous pour résoudre ce problème. Nous vous enverrons une notification soit détaillant les mesures que vous devrez prendre soit avec plus d’informations sur la façon de contacter l’équipe d’ingénierie ou de support technique d’Azure.  
- **Récupération assistée :** Un événement est survenu et les ingénieurs ont confirmé que l’impact vous affectait toujours. L’ingénierie devra travailler avec vous directement pour restaurer vos services.  
- **Incident :** Un événement ayant un impact sur un service affectant actuellement une ou plusieurs des ressources de votre abonnement.  
- **Maintenance :** Il s’agit d’une notification vous informant d’une activité de maintenance planifiée qui peut avoir un impact sur une ou plusieurs ressources de votre abonnement.  
- **Informations :** De temps de temps, nous pouvons vous envoyer des notifications pour vous informer sur les optimisations potentielles qui peuvent améliorer votre utilisation des ressources.  
- **Sécurité :** Des informations urgentes liées à la sécurité concernant vos solutions s’exécutant sur Azure.

Chaque notification d’intégrité de service contiendra des détails sur l’étendue et l’impact sur vos ressources. Les détails incluront ce qui suit :

Nom de la propriété | Description
-------- | -----------
channels | Est une des valeurs suivantes : « Admin », « Operation »
correlationId | Est généralement un GUID au format chaîne. Les événements qui appartiennent à la même action uber partagent généralement le même correlationId.
eventDataId | Est l’identificateur unique d’un événement
eventName | Est le titre de la campagne
minimal | Niveau de l’événement. Une des valeurs suivantes : Critical, Error, Warning, Informational et Verbose
resourceProviderName | Nom du fournisseur de ressources de la ressource affectée.
resourceType| Le type de la ressource affectée
subStatus | Il s’agit généralement du code d’état HHTP de l’appel REST correspondant, mais également d’autres chaînes décrivant un sous-état, comme ces valeurs courantes : OK (Code d’état HTTP : 200), Created (Code d’état HTTP : 201), Accepted (Code d’état HTTP : 202), No content (Code d’état HTTP : 204), Bad Request (Code d’état HTTP : 400), Not found (Code d’état HTTP : 404), Conflict (Code d’état HTTP : 409), Internal Server Error (Code d’état HTTP : 500), Service Unavailable (Code d’état HTTP : 503), Gateway Timeout (Code d’état HTTP : 504).
eventTimestamp | Horodatage lorsque l’événement a été généré par le service Azure traitant la demande correspondant à l’événement.
submissionTimestamp |   Horodatage lorsque l’événement est devenu disponible pour l’interrogation.
subscriptionId | L’abonnement Azure dans lequel l’événement est consigné
status | Chaîne décrivant l’état de l’opération. Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.
operationName | Nom de l’opération.
category | « ServiceHealth »
resourceId | ID de ressource de la ressource affectée.
Properties.title | Le titre localisé pour cette communication. La langue par défaut est l’anglais.
Properties.communication | Les détails localisés de la communication avec le balisage HTML. L’anglais est la langue par défaut.
Properties.incidentType | valeurs possibles : AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifie l’incident associé à cet événement. Cela permet de mettre en corrélation les événements liés à un incident.
Properties.impactedServices | Un échappement blob JSON qui décrit les services et régions qui sont affectés par l’incident. Une liste de services, chacun possédant un ServiceName et une liste d’ImpactedRegions, chacune ayant un RegionName.
Properties.defaultLanguageTitle | La communication en anglais
Properties.defaultLanguageContent | La communication en anglais en tant que HTML ou texte brut
Properties.stage | Les valeurs possibles pour AssistedRecovery, ActionRequired, Information, Incident et Security sont Active, Resolved. Pour Maintenance, les valeurs possibles sont Active, Planned, InProgress, Canceled, Rescheduled, Resolved et Complete
Properties.communicationId | La communication associée à cet événement.


## <a name="viewing-your-service-health-notifications-in-the-azure-portal"></a>Affichage de vos notifications d’intégrité de service dans le portail Azure
1.  Dans le [portail](https://portal.azure.com), accédez au service **Monitor**

    ![Surveiller](./media/monitoring-service-notifications/home-monitor.png)
2.  Cliquez sur l’option **Monitor** pour ouvrir le panneau Monitor. Ce panneau rassemble tous vos paramètres de surveillance et données dans une vue consolidée. Il ouvre d’abord la section **Journal d’activité** .

3.  Cliquez maintenant sur le service **Notifications de service**

    ![Surveiller](./media/monitoring-service-notifications/service-health-summary.png)
4.  Cliquez sur un des éléments de ligne pour afficher plus de détails

5. Cliquez sur l’opération **+ Ajouter une alerte de journal d’activité** pour recevoir des notifications pour vous assurer que vous êtes informé des futures notifications de service de ce type. Pour en savoir plus sur la configuration des alertes sur les notifications de service, [cliquez ici](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Étapes suivantes :
Recevez des [notifications d'alerte lorsqu'une notification d’intégrité de service](monitoring-activity-log-alerts-on-service-notifications.md) est publiée  
En savoir plus sur les [alertes du journal d’activité](monitoring-activity-log-alerts.md)
