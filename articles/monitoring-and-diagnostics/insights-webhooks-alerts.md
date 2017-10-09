---
title: "webhooks aaaConfigure sur les alertes de métrique Azure | Documents Microsoft"
description: "Rediriger les systèmes non-Azure tooother alertes Azure."
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Configurer un webhook sur une alerte de métrique Azure
Autoriser le Webhooks vous tooroute Azure pour les actions de post-traitement ou personnalisées, les systèmes de notification tooother d’alerte. Vous pouvez utiliser un webhook sur une alerte tooroute il tooservices qui envoient des SMS, enregistrer les bogues, notifier une équipe via les services de messagerie/conversation qui ou n’importe quel nombre d’autres actions. Cet article décrit comment tooset un webhook sur une alerte de métrique Azure et le charge hello hello HTTP POST tooa webhook ressemble. Pour plus d’informations sur le programme d’installation hello et le schéma d’une alerte de journal des activités Azure (alerte sur les événements), [cette page s’affiche à la place](insights-auditlog-to-webhook-email.md).

Azure alertes HTTP POST hello contenu de l’alerte au format JSON, schéma défini ci-dessous, tooa webhook URI que vous fournissez lors de la création d’alerte de hello. Cet URI doit être un point de terminaison HTTP ou HTTPS valide. Azure publie une entrée par demande lorsqu’une alerte est activée.

## <a name="configuring-webhooks-via-hello-portal"></a>Configuration des webhooks via le portail de hello
Vous pouvez ajouter ou mettre à jour hello webhook URI sur l’écran hello créer/mettre à jour les alertes Bonjour [portal](https://portal.azure.com/).

![Ajouter une règle d’alerte](./media/insights-webhooks-alerts/Alertwebhook.png)

Vous pouvez également configurer un webhook de tooa toopost alerte URI à l’aide de hello [applets de commande PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [inter-plateformes CLI](insights-cli-samples.md#work-with-alerts), ou [API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Authentification hello webhook
Hello webhook peut s’authentifier à l’aide d’autorisation basée sur le jeton. Hello webhook URI est, par exemple enregistré avec un ID de jeton. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Schéma de la charge utile
Hello opération POST contient hello suivant charge utile JSON et schéma pour toutes les alertes métrique.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Champ | Obligatoire | Ensemble fixe de valeurs | Remarques |
|:--- |:--- |:--- |:--- |
| status |O |"Activated", "Resolved" |État d’alerte de hello basés sur les conditions de hello que vous avez défini. |
| context |O | |contexte de l’alerte Hello. |
| timestamp |O | |heure de Hello à quels hello alerte a été déclenchée. |
| id |O | |Chaque règle d’alerte possède un ID unique. |
| name |O | |nom de l’alerte Hello. |
| description |O | |Description de l’alerte de hello. |
| conditionType |O |"Metric", "Event" |Deux types d’alertes sont pris en charge. L’une basée sur une condition de métriques et hello autres en fonction d’un événement dans le journal d’activité de hello. Utilisez cette valeur toocheck si alerte de hello est basée sur la mesure ou un événement. |
| condition |O | |Bonjour toocheck des champs spécifiques pour selon hello conditionType. |
| metricName |Pour les alertes de métrique | |analyse du nom Hello de métrique hello qui définit quelle règle hello. |
| metricUnit |Pour les alertes de métrique |« Bytes », « BytesPerSecond », « Count », « CountPerSecond », « Percent », « Seconds » |unité de Hello autorisée dans la mesure de hello. [Les valeurs autorisées sont répertoriées ici](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |Pour les alertes de métrique | |valeur réelle de Hello de métrique hello ayant provoqué l’alerte de hello. |
| threshold |Pour les alertes de métrique | |valeur de seuil Hello à quels hello alerte est activée. |
| windowSize |Pour les alertes de métrique | |Hello période de temps qui est l’activité d’alerte toomonitor utilisé selon le seuil de hello. Doit être comprise entre 5 minutes et 1 jour. Le format de la durée répond à la norme ISO 8601. |
| timeAggregation |Pour les alertes de métrique |« Average », « Last », « Maximum », « Minimum », « None », « Total » |Comment les données de hello collectées doivent être combinées au fil du temps. valeur par défaut de Hello est moyenne. [Les valeurs autorisées sont répertoriées ici](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| operator |Pour les alertes de métrique | |Hello opérateur utilisé toocompare hello actuel données métriques toohello seuil défini. |
| subscriptionId |O | |ID d’abonnement Azure. |
| resourceGroupName |O | |Nom du groupe de ressources hello pour hello incidence sur la ressource. |
| resourceName |O | |Nom de ressource de hello affectées les ressources. |
| resourceType |O | |Type de ressource de hello affectées les ressources. |
| resourceId |O | |ID de ressource de hello affectées les ressources. |
| resourceRegion |O | |Région ou l’emplacement du hello affectées des ressources. |
| portalLink |O | |Page Résumé lien direct toohello ressource portail. |
| properties |N |Facultatif |Jeu de `<Key, Value>` paires (c'est-à-dire `Dictionary<String, String>`) qui inclut des détails sur l’événement hello. champ de propriétés Hello est facultatif. Dans une interface utilisateur ou à une logique basée sur une application flux de travail personnalisé, les utilisateurs peuvent entrer clé/valeur qui peut être passée via la charge utile de hello. Hello autre façon toopass propriétés personnalisées toohello arrière webhook est via l’uri du webhook hello elle-même (en tant que paramètres de requête) |

> [!NOTE]
> champ de propriétés Hello ne peut être définie à l’aide de hello [API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur les alertes de Azure et de webhooks vidéo de hello [intégrer Azure Alerts à PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Exécuter des scripts Azure Automation (Runbooks) sur des alertes Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Utilisez l’application logique toosend SMS via Twilio à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Utilisez l’application logique toosend un message de marge d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Utilisez l’application logique toosend un tooan message file d’attente Azure à partir d’une alerte Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
