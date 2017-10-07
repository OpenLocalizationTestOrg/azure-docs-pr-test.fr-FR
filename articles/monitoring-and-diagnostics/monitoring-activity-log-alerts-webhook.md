---
title: "schéma de webhook aaaUnderstand hello utilisée dans les alertes de journal d’activité | Documents Microsoft"
description: "En savoir plus sur le schéma hello Hello JSON est validé l’URL du webhook tooa lorsqu’une alerte de journal d’activité active."
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Webhook des alertes du journal d’activité Azure
Dans le cadre de définition de hello d’un groupe d’actions, vous pouvez configurer webhook points de terminaison tooreceive activité journal des notifications d’alerte. Avec le webhooks, vous pouvez acheminer ces systèmes de tooother des notifications pour les actions de post-traitement ou personnalisées. Cet article explique le charge hello hello HTTP POST tooa webhook ressemble à.

Pour plus d’informations sur les alertes de journal d’activité, consultez Comment trop[créer des alertes de journal des activités Windows Azure](monitoring-activity-log-alerts.md).

Pour plus d’informations sur les groupes d’actions, consultez Comment trop[créer des groupes d’actions](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>Authentifier hello webhook
Hello webhook peut éventuellement utiliser d’autorisation basée sur un jeton pour l’authentification. Hello webhook URI est enregistré avec un ID de jeton, par exemple, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Schéma de la charge utile
charge utile JSON de Hello contenue dans hello opération POST diffère en fonction de champ de data.context.activityLog.eventSource de charge utile de hello.

###<a name="common"></a>Courant
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Administratif
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Pour obtenir des informations spécifiques au sujet des schémas des alertes du journal d’activité sur les notifications d’intégrité du service, consultez la page [Notifications d’intégrité du service](monitoring-service-notifications.md).

Pour plus d’informations de schéma spécifique sur toutes les autres alertes de journal d’activité, consultez [vue d’ensemble du journal des activités Windows Azure hello](monitoring-overview-activity-logs.md).

| Nom de l'élément | Description |
| --- | --- |
| status |Utilisé pour les alertes de métrique. Toujours défini trop « activé » pour les alertes de journal d’activité. |
| context |Contexte d’événement de hello. |
| resourceProviderName |le fournisseur de ressources Hello Hello incidence sur la ressource. |
| conditionType |Toujours défini sur « Event ». |
| name |Nom de règle d’alerte hello. |
| id |ID de ressource d’alerte de hello. |
| description |Description de l’alerte définie lors de l’alerte de hello est créée. |
| subscriptionId |ID d’abonnement Azure. |
| timestamp |Heure à quels hello événement a été généré par hello service Azure qui a traité la demande de hello. |
| resourceId |ID de ressource de hello affectées les ressources. |
| resourceGroupName |Nom du groupe de ressources hello pour hello incidence sur la ressource. |
| properties |Jeu de `<Key, Value>` paires (autrement dit, `Dictionary<String, String>`) qui inclut des détails sur l’événement hello. |
| event |Élément qui contient des métadonnées sur l’événement hello. |
| autorisation |propriétés de contrôle d’accès en fonction du rôle Hello d’événement de hello. Ces propriétés incluent généralement l’action de hello, le rôle de hello et étendue de hello. |
| category |Catégorie d’événement de hello. Les valeurs prises en charge sont : Administrative, Alert, Security, ServiceHealth et Recommendation. |
| caller |Adresse de messagerie de l’utilisateur hello qui a effectué l’opération de hello, revendication UPN ou revendication SPN basée sur la disponibilité. Peut être null pour certains appels système. |
| correlationId |Généralement un GUID au format chaîne. Les événements avec l’ID de corrélation appartiennent toohello même action plus importante et partagent généralement un ID de corrélation. |
| eventDescription |Description de texte statique de l’événement de hello. |
| eventDataId |Identificateur unique de l’événement de hello. |
| eventSource |Nom de hello service Azure ou infrastructure que l’événement hello généré. |
| httpRequest |Hello demande inclut généralement hello clientRequestId clientIpAddress et la méthode HTTP (par exemple, PUT). |
| level |Une des valeurs suivantes de hello : critique, erreur, avertissement, information et Verbose. |
| operationId |Généralement GUID partagé entre les événements hello correspondant toosingle opération. |
| operationName |Nom de l’opération de hello. |
| properties |Propriétés d’événement de hello. |
| status |Chaîne. État de l’opération de hello. Les valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active et Resolved. |
| subStatus |Inclut généralement le code d’état HTTP hello d’appel REST hello correspondant. Peut également inclure d’autres chaînes décrivant un sous-état. Les valeurs courantes sont : OK (Code d’état HTTP : 200), Created (Code d’état HTTP : 201), Accepted (Code d’état HTTP : 202), No Content (Code d’état HTTP : 204), Bad Request (Code d’état HTTP : 400), Not Found (Code d’état HTTP : 404), Conflict (Code d’état HTTP : 409), Internal Server Error (Code d’état HTTP : 500), Service Unavailable (Code d’état HTTP : 503) et Gateway Timeout (Code d’état HTTP : 504). |

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur le journal d’activité hello](monitoring-overview-activity-logs.md).
* [Exécuter des scripts Azure Automation (Runbooks) sur des alertes Azure](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Utiliser un toosend d’application logique SMS via Twilio à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Cet exemple est pour les alertes de métriques, mais il peut être modifié toowork avec une alerte de journal d’activité.
* [Utiliser un toosend d’application logique un message de marge d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Cet exemple est pour les alertes de métriques, mais il peut être modifié toowork avec une alerte de journal d’activité.
* [Utiliser un toosend d’application logique de file d’attente un message de tooan Azure à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Cet exemple est pour les alertes de métriques, mais il peut être modifié toowork avec une alerte de journal d’activité.
