---
title: "aaaCall un webhook sur les alertes du journal des activités Azure | Documents Microsoft"
description: "Services tooother itinéraire activité journal des événements pour les actions personnalisées. Par exemple envoyer des SMS, journaliser des bogues ou notifier une équipe via un service de chat/messagerie."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Appeler un webhook sur une alerte de journal d’activité Azure
Autoriser le Webhooks vous tooroute Azure pour les actions de post-traitement ou personnalisées, les systèmes de notification tooother d’alerte. Vous pouvez utiliser un webhook sur une alerte tooroute il tooservices qui envoient des SMS, enregistrer les bogues, notifier une équipe via les services de messagerie/conversation qui ou n’importe quel nombre d’autres actions. Cet article décrit comment tooset un toobe webhook appelée quand un déclenche alerte du journal des activités Azure. Il montre également le charge hello hello HTTP POST tooa webhook ressemble à. Pour plus d’informations sur le programme d’installation hello et le schéma d’une alerte de métrique Azure, [cette page s’affiche à la place](insights-webhooks-alerts.md). Vous pouvez également configurer un e-mail d’alerte toosend journal d’activité lors de l’activation.

> [!NOTE]
> Cette fonctionnalité est actuellement en version préliminaire et sera supprimée à un moment donné dans hello futures.
>
>

Vous pouvez configurer une alerte de journal d’activité à l’aide de hello [applets de commande PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [inter-plateformes CLI](insights-cli-samples.md#work-with-alerts), ou [API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn933805.aspx). Actuellement, vous ne peut pas définir une à l’aide de hello portail Azure.

## <a name="authenticating-hello-webhook"></a>Authentification hello webhook
Hello webhook peut s’authentifier à l’aide d’une des méthodes suivantes :

1. **Autorisation basée sur le jeton** -hello webhook URI est enregistré avec un ID de jeton, par exemple,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Autorisation de base** -hello webhook URI est enregistré avec un nom d’utilisateur et un mot de passe, par exemple,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>Schéma de la charge utile
Hello opération POST contient hello suivant charge utile JSON et schéma pour toutes les alertes le journal d’activité. Ce schéma est semblable toohello une utilisée par les alertes basées sur la mesure.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Nom de l’élément | Description |
| --- | --- |
| status |Utilisé pour les alertes de métrique. Toujours défini trop « activé » pour les alertes de journal d’activité. |
| context |Contexte d’événement de hello. |
| resourceProviderName |le fournisseur de ressources Hello Hello incidence sur la ressource. |
| conditionType |Toujours défini sur « Event ». |
| name |Nom de règle d’alerte hello. |
| id |ID de ressource d’alerte de hello. |
| description |Description de l’alerte en tant qu’ensemble lors de la création d’alerte de hello. |
| subscriptionId |ID d’abonnement Azure. |
| timestamp |Heure à quels hello événement a été généré par hello service Azure qui a traité la demande de hello. |
| resourceId |ID de ressource de hello affectées les ressources. |
| resourceGroupName |Nom du groupe de ressources hello pour hello affectés des ressources |
| properties |Jeu de `<Key, Value>` paires (c'est-à-dire `Dictionary<String, String>`) qui inclut des détails sur l’événement hello. |
| event |Élément contenant les métadonnées sur l’événement hello. |
| autorisation |propriétés RBAC Hello d’événement de hello. Il s’agit généralement hello « action », « rôle » et hello « étendue ». |
| category |Catégorie d’événement de hello. Les valeurs prises en charge sont : Administrative, Alert, Security, ServiceHealth, Recommendation. |
| caller |Adresse de messagerie de l’utilisateur hello qui a effectué l’opération de hello, revendication UPN ou revendication SPN basée sur la disponibilité. Peut être null pour certains appels système. |
| correlationId |Généralement un GUID au format chaîne. Les événements avec l’ID de corrélation appartiennent toohello même action plus importante et partagent généralement un ID de corrélation. |
| eventDescription |Description de texte statique de l’événement de hello. |
| eventDataId |Identificateur unique de l’événement de hello. |
| eventSource |Nom de hello service Azure ou infrastructure que l’événement hello généré. |
| httpRequest |Inclut généralement hello « clientRequestId », « clientIpAddress » et « method » (méthode HTTP PUT, par exemple). |
| level |Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires ». |
| operationId |Généralement GUID partagé entre les événements hello correspondant toosingle opération. |
| operationName |Nom de l’opération de hello. |
| properties |Propriétés d’événement de hello. |
| status |Chaîne. État de l’opération de hello. Les valeurs courantes sont : « Started », « In Progress », « Succeeded », « Failed », « Active », « Resolved ». |
| subStatus |Inclut généralement le code d’état HTTP hello d’appel REST hello correspondant. Il peut également inclure d’autres chaînes décrivant un sous-état. Les valeurs courantes sont : OK (Code d’état HTTP : 200), Created (Code d’état HTTP : 201), Accepted (Code d’état HTTP : 202), No Content (Code d’état HTTP : 204), Bad Request (Code d’état HTTP : 400), Not Found (Code d’état HTTP : 404), Conflict (Code d’état HTTP : 409), Internal Server Error (Code d’état HTTP : 500), Service Unavailable (Code d’état HTTP : 503), Gateway Timeout (Code d’état HTTP : 504). |

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello journal d’activité](monitoring-overview-activity-logs.md)
* [Exécuter des scripts Azure Automation (Runbooks) sur des alertes Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Utilisez l’application logique toosend SMS via Twilio à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Cet exemple est pour les alertes de métriques, mais peut être modifiée toowork avec une alerte de journal d’activité.
* [Utilisez l’application logique toosend un message de marge d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Cet exemple est pour les alertes de métriques, mais peut être modifiée toowork avec une alerte de journal d’activité.
* [Utilisez l’application logique toosend un tooan message file d’attente Azure à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Cet exemple est pour les alertes de métriques, mais peut être modifiée toowork avec une alerte de journal d’activité.
