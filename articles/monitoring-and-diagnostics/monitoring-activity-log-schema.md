---
title: "aaaAzure schéma événements des journaux d’activité | Documents Microsoft"
description: "Comprendre le schéma d’événement hello pour les données émises dans le journal d’activité de hello"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Schéma d’événements du journal d’activité
Hello **journal des activités Azure** est un journal qui fournit un aperçu de tous les événements de niveau d’abonnement qui se sont produites dans Azure. Cet article décrit le schéma d’événement hello par catégorie de données.

## <a name="administrative"></a>Administratif
Cette catégorie contient les enregistrement hello de tous les créer, les opérations de mise à jour, de suppression et d’action effectuée par le biais du Gestionnaire de ressources. Exemples de hello les types d’événements que vous verriez dans cette catégorie incluent « créer la machine virtuelle » et « supprimer un groupe de sécurité réseau « chaque action effectuée par un utilisateur ou l’application à l’aide du Gestionnaire de ressources est modelée comme une opération sur un type particulier. Si le type d’opération hello est écrire, supprimer, ou Action, enregistrements hello de début de hello et réussite ou Échec de cette opération sont enregistrées dans la catégorie Administrative de hello. catégorie Administrative de Hello inclut également toutes les modifications de contrôle d’accès toorole dans un abonnement.

### <a name="sample-event"></a>Exemple d’événement
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Description des propriétés
| Nom de l’élément | Description |
| --- | --- |
| autorisation |Objet BLOB de propriétés RBAC de l’événement de hello. Inclut généralement les propriétés « action », « rôle » et « portée » hello. |
| caller |Adresse de messagerie de l’utilisateur de hello qui a effectué les opération hello, revendication UPN ou revendication SPN basée sur la disponibilité. |
| channels |Une des valeurs suivantes de hello : « Admin », « Opération » |
| réclamations |un jeton JWT Hello utilisés par Active Directory tooauthenticate hello utilisateur ou l’application tooperform cette opération dans le Gestionnaire de ressources. |
| correlationId |Généralement, un GUID au format de chaîne hello. Les événements qui partagent un ID de corrélation appartiennent toohello même action uber. |
| description |Description textuelle statique d’un événement. |
| eventDataId |Identificateur unique d’un événement. |
| httpRequest |BLOB hello décrivant requête Http. Inclut généralement hello « clientRequestId », « clientIpAddress » et « method » (méthode HTTP. Par exemple, PUT). |
| level |Niveau d’événement de hello. Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires » |
| resourceGroupName |Nom du groupe de ressources hello pour hello incidence sur la ressource. |
| resourceProviderName |Nom du fournisseur de ressources hello pour hello affectées les ressources |
| resourceId |Id de ressource de hello affectées les ressources. |
| operationId |Un GUID est partagé entre les événements hello qui correspondent tooa une seule opération. |
| operationName |Nom de l’opération de hello. |
| properties |Jeu de `<Key, Value>` paires (autrement dit, un dictionnaire) hello décrivant les événements hello. |
| status |Chaîne décrivant l’état hello d’opération de hello. Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus |Généralement hello le code d’état HTTP de hello correspondant appel REST, mais peut également inclure d’autres chaînes décrivant un sous-état, telles que ces valeurs courantes : OK (Code d’état HTTP : 200), créé (Code d’état HTTP : 201), accepté (Code d’état HTTP : 202), aucun contenu (HTTP Code d’état : 204), demande incorrecte (Code d’état HTTP : 400), il est introuvable (Code d’état HTTP : 404), conflit (Code d’état HTTP : 409), erreur interne au serveur (Code d’état HTTP : 500), Service indisponible (Code d’état HTTP : 503), délai d’attente de la passerelle (Code d’état HTTP : 504). |
| eventTimestamp |Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant. |
| submissionTimestamp |Horodatage lors de l’événement de hello sont devenues disponible pour l’interrogation. |
| subscriptionId |ID d’abonnement Azure. |

## <a name="service-health"></a>État d’intégrité du service
Cette catégorie contient un enregistrement hello n’importe quel contrôle d’intégrité des incidents de services qui se sont produites dans Azure. Un exemple de type hello d’événement que vous verriez dans cette catégorie est « SQL Azure dans l’est des États-Unis rencontre des temps d’arrêt. » Événements de contrôle d’intégrité de service existe cinq types : Action requise, récupération d’assistance, Incident, Maintenance, informations ou la sécurité et n’apparaissent que si vous avez une ressource dans l’abonnement hello qui est affecté par l’événement de hello.

### <a name="sample-event"></a>Exemple d’événement
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Description des propriétés
Nom de l’élément | Description
-------- | -----------
channels | Est une des valeurs suivantes de hello : « Admin », « Opération »
correlationId | Est généralement un GUID au format de chaîne hello. Événements appartenant toohello même action uber partagent généralement hello même correlationId.
description | Description de l’événement de hello.
eventDataId | Bonjour à l’identificateur unique d’un événement.
eventName | titre de Hello d’événement de hello.
level | Niveau d’événement de hello. Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires »
resourceProviderName | Nom du fournisseur de ressources hello pour hello incidence sur la ressource. S’il est inconnu, cette option sera nulle.
resourceType| type Hello de ressource de hello affectées les ressources. S’il est inconnu, cette option sera nulle.
subStatus | Généralement nul pour les événements de l’état d’intégrité du service.
eventTimestamp | Horodatage lors de l’événement du journal hello a été générée et envoyée toohello journal d’activité.
submissionTimestamp |   Horodatage lors de l’événement de hello est devenu disponible dans le journal d’activité de hello.
subscriptionId | Bonjour abonnement Azure dans laquelle cet événement a été enregistré.
status | Chaîne décrivant l’état hello d’opération de hello. Certaines valeurs courantes sont : actif, résolu.
operationName | Nom de l’opération de hello. Généralement Microsoft.ServiceHealth/incident/action.
category | « ServiceHealth »
resourceId | Id de ressource de hello une incidence sur la ressource, s’il est connu. L’ID d’abonnement est fourni dans le cas contraire.
Properties.title | Hello titre localisé pour cette communication. L’anglais est la langue par défaut de hello.
Properties.communication | Hello localisées des détails de communication hello par un balisage HTML. L’anglais est la valeur par défaut hello.
Properties.incidentType | valeurs possibles : AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifie l’incident hello que cet événement est associé. Utilisez cet incident de toocorrelate hello événements tooan connexes.
Properties.impactedServices | Un séquence d’échappement blob JSON qui décrit les services hello et les régions qui sont affectées par l’incident de hello. Une liste de services, chacun possédant un ServiceName et une liste d’ImpactedRegions, chacune ayant un RegionName.
Properties.defaultLanguageTitle | communication Hello en anglais
Properties.defaultLanguageContent | communication Hello en anglais en tant que balisage html ou texte brut
Properties.stage | Les valeurs possibles pour AssistedRecovery, ActionRequired, Information, Incident et Security sont Active, Resolved. Pour Maintenance, les valeurs possibles sont Active, Planned, InProgress, Canceled, Rescheduled, Resolved et Complete
Properties.communicationId | communication de Hello cet événement est associé.

## <a name="alert"></a>Alerte
Cette catégorie contient un enregistrement hello de toutes les activations d’alertes Azure. Un exemple de type hello d’événement que vous verriez dans cette catégorie est « % du processeur sur myVM a été plus de 80 pour hello 5 dernières minutes. » Une variété de systèmes Azure possèdent un concept d’alertes : vous pouvez définir une règle quelconque et recevoir une notification lorsque les conditions correspondent à cette règle. Chaque fois qu’un type d’alerte Azure pris en charge 'active,' ou hello conditions sont rempli toogenerate une notification, un enregistrement de l’activation de hello est envoyé également catégorie toothis Hello journal d’activité.

### <a name="sample-event"></a>Exemple d’événement

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Description des propriétés
| Nom de l’élément | Description |
| --- | --- |
| caller | Toujours Microsoft.Insights/alertRules |
| channels | Toujours « Admin, opération » |
| réclamations | Objet blob de JSON avec hello SPN (nom principal de service), ou une ressource de type, de moteur d’alerte hello. |
| correlationId | Un GUID au format de chaîne hello. |
| description |Description de texte statique de l’événement d’alerte hello. |
| eventDataId |Identificateur unique de l’événement d’alerte hello. |
| level |Niveau d’événement de hello. Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires » |
| resourceGroupName |Nom du groupe de ressources hello pour hello affectée ressource s’il s’agit d’une alerte de métrique. Pour les autres types d’alerte, il s’agit de nom de hello hello du groupe de ressources qui contient l’alerte hello lui-même. |
| resourceProviderName |Nom du fournisseur de ressources hello pour hello affectée ressource s’il s’agit d’une alerte de métrique. Pour les autres types d’alerte, il s’agit de nom de hello de fournisseur de ressources hello pour alerte hello lui-même. |
| resourceId | Nom de l’ID de ressource hello pour hello affectée ressource s’il s’agit d’une alerte de métrique. Pour les autres types d’alerte, il s’agit de hello les ID de ressource de ressource d’alerte hello elle-même. |
| operationId |Un GUID est partagé entre les événements hello qui correspondent tooa une seule opération. |
| operationName |Nom de l’opération de hello. |
| properties |Jeu de `<Key, Value>` paires (autrement dit, un dictionnaire) hello décrivant les événements hello. |
| status |Chaîne décrivant l’état hello d’opération de hello. Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | Généralement, nul pour les alertes. |
| eventTimestamp |Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant. |
| submissionTimestamp |Horodatage lors de l’événement de hello sont devenues disponible pour l’interrogation. |
| subscriptionId |ID d’abonnement Azure. |

### <a name="properties-field-per-alert-type"></a>Champ Propriétés par type d’alerte
champ de propriétés Hello contient des valeurs différentes en fonction de la source de hello d’événement d’alerte hello. Deux fournisseurs d’événements d’alertes courants sont les alertes du journal d’activité et les alertes métriques.

#### <a name="properties-for-activity-log-alerts"></a>Propriétés pour les alertes du journal d’activité
| Nom de l’élément | Description |
| --- | --- |
| properties.subscriptionId | ID d’abonnement Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé. |
| properties.eventDataId | Hello des ID de données d’événement à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé. |
| properties.resourceGroup | groupe de ressources Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé. |
| properties.resourceId | ID de ressource Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé. |
| properties.eventTimestamp | Bonjour horodatage d’un événement de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé. |
| properties.operationName | nom de l’opération Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé. |
| Properties.Status | état de Hello à partir de l’événement de journal d’activité hello qui a provoqué cette toobe de règle d’alerte de journal activité activé.|

#### <a name="properties-for-metric-alerts"></a>Propriétés des alertes métriques
| Nom de l’élément | Description |
| --- | --- |
| Propriétés. RuleUri | ID de ressource de hello métrique règle d’alerte lui-même. |
| Propriétés. Nom_règle | nom Hello de règle d’alerte métrique hello. |
| Propriétés. RuleDescription | description de Hello de règle d’alerte métrique hello (tel que défini dans la règle d’alerte hello). |
| Propriétés. Seuil | valeur de seuil Hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello. |
| properties.WindowSizeInMinutes | taille de la fenêtre Hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello. |
| properties.Aggregation | type d’agrégation Hello défini dans la règle d’alerte métrique hello. |
| properties.Operator | opérateur conditionnel de Hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello. |
| properties.MetricName | nom de la métrique Hello de métrique hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello. |
| properties.MetricUnit | unité de mesure Hello pour métrique hello utilisée dans l’évaluation de hello de règle d’alerte métrique hello. |

## <a name="autoscale"></a>Autoscale
Cette catégorie contient un enregistrement hello de toute opération toohello connexes d’événements du moteur de mise à l’échelle hello selon les paramètres d’échelle automatique que vous avez défini dans votre abonnement. Un exemple de type hello d’événement que vous verriez dans cette catégorie est « Mise à l’échelle mise à l’échelle de l’échec de l’action. » À l’aide de la mise à l’échelle, vous pouvez automatiquement montée en puissance parallèle ou mettre à l’échelle dans hello nombre d’instances d’un type de ressource pris en charge basée sur l’heure du jour et/ou la charge des données (métriques) à l’aide d’un paramètre de mise à l’échelle. En cas de hello conditions sont remplies tooscale vers le haut ou vers le bas, hello démarrer et a réussi, ou les événements ayant échouées seront enregistrés dans cette catégorie.

### <a name="sample-event"></a>Exemple d’événement
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Description des propriétés
| Nom de l’élément | Description |
| --- | --- |
| caller | Always Microsoft.Insights/autoscaleSettings |
| channels | Toujours « Admin, opération » |
| réclamations | Objet blob de JSON avec hello type SPN (nom principal de service) ou des ressources, du moteur de mise à l’échelle hello. |
| correlationId | Un GUID au format de chaîne hello. |
| description |Description de texte statique d’événement de mise à l’échelle hello. |
| eventDataId |Identificateur unique de l’événement de mise à l’échelle hello. |
| level |Niveau d’événement de hello. Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires » |
| resourceGroupName |Nom du groupe de ressources hello pour le paramètre de mise à l’échelle hello. |
| resourceProviderName |Nom du fournisseur de ressources hello pour le paramètre de mise à l’échelle hello. |
| resourceId |Id de ressource du paramètre de mise à l’échelle hello. |
| operationId |Un GUID est partagé entre les événements hello qui correspondent tooa une seule opération. |
| operationName |Nom de l’opération de hello. |
| properties |Jeu de `<Key, Value>` paires (autrement dit, un dictionnaire) hello décrivant les événements hello. |
| properties.Description | Description détaillée des opérations en cours dans le moteur de mise à l’échelle hello. |
| properties.ResourceName | ID de ressource de hello affectées les ressources (hello des ressources sur le hello à l’échelle a été effectuée.) |
| properties.OldInstancesCount | nombre de Hello d’instances avant l’action de mise à l’échelle hello a pris effet. |
| properties.NewInstancesCount | nombre de Hello d’instances une fois que l’action de mise à l’échelle hello a pris effet. |
| properties.LastScaleActionTime | horodatage de Hello de lorsque l’action de mise à l’échelle hello s’est produite. |
| status |Chaîne décrivant l’état hello d’opération de hello. Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | Généralement, nul pour la mise à l’échelle automatique. |
| eventTimestamp |Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant. |
| submissionTimestamp |Horodatage lors de l’événement de hello sont devenues disponible pour l’interrogation. |
| subscriptionId |ID d’abonnement Azure. |

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello journal d’activité (anciennement les journaux d’Audit)](monitoring-overview-activity-logs.md)
* [Flux tooEvent du journal des activités Azure hello concentrateurs](monitoring-stream-activity-logs-event-hubs.md)
