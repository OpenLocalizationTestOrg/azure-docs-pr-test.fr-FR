---
title: aaaUsing OMS journal Analytique alerte REST API
description: "Hello journal Analytique alerte REST API vous permet de toocreate et gérer les alertes dans Analytique de journal qui fait partie d’Operations Management Suite (OMS).  Cet article fournit des détails de hello API et plusieurs exemples pour effectuer différentes opérations."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Créer et gérer des règles d’alerte dans Log Analytics avec l’API REST
Hello journal Analytique alerte REST API vous permet de toocreate et gérer les alertes Operations Management Suite (OMS).  Cet article fournit des détails de hello API et plusieurs exemples pour effectuer différentes opérations.

Hello API REST de journal Analytique Search est RESTful et sont accessibles via les REST API Azure Resource Manager de hello. Dans ce document vous trouverez des exemples où hello API est accessible à partir d’une ligne de commande PowerShell à l’aide [ARMClient](https://github.com/projectkudu/ARMClient), un outil de ligne de commande open source qui simplifie l’appel hello API Azure Resource Manager. utilisation de Hello d’ARMClient et de PowerShell est une des nombreuses options de tooaccess hello API de recherche Analytique de journal. Grâce à ces outils, vous pouvez utiliser des espaces de travail hello API RESTful Azure Resource Manager toomake appelle tooOMS et exécuter des commandes de recherche de. Hello API produira tooyou de résultats de recherche au format JSON, ce qui vous toouse résultats de la recherche hello de différentes façons par programme.

## <a name="prerequisites"></a>Composants requis
Actuellement, les alertes peuvent être créées uniquement avec une recherche enregistrée dans Log Analytics.  Vous pouvez faire référence toohello [API REST de recherche journal](log-analytics-log-search-api.md) pour plus d’informations.

## <a name="schedules"></a>Planifications
Une recherche enregistrée peut avoir une ou plusieurs planifications. Hello planification définit la fréquence à laquelle hello recherche est exécutée et intervalle de temps hello sur les critères de hello est identifiée.
Planifications ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Intervalle |La fréquence à laquelle hello recherche est exécutée. Exprimée en minutes. |
| QueryTimeSpan |intervalle de temps Hello sur quel hello critères est évaluée. Doit être supérieure à intervalle égal tooor. Exprimée en minutes. |
| Version |Hello version API utilisée.  Actuellement, il doit toujours être défini too1. |

Par exemple, considérez une requête d’événement avec Interval défini sur 15 minutes et QueryTimeSpan sur 30 minutes. Dans ce cas, les requêtes hello sont exécuté toutes les 15 minutes, et se déclenchera une alerte si les critères de hello suite tooresolve tootrue sur un intervalle de 30 minutes.

### <a name="retrieving-schedules"></a>Récupération des planifications
Méthode tooretrieve d’obtenir hello d’utiliser toutes les planifications d’une recherche enregistrée.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Hello d’utilisation Get (méthode) avec un tooretrieve ID de planification une planification particulière d’une recherche enregistrée.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

Voici un exemple de réponse pour une planification.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Création d'une planification
Utilisez la méthode de Put de hello avec un toocreate ID de planification unique une planification.  Notez que deux planifications ne peut pas avoir hello même ID même s’ils sont associés avec différentes recherches enregistrées.  Lorsque vous créez une planification dans la console OMS hello, un GUID est créé pour l’ID de planification hello.

> [!NOTE]
> nom de Hello pour toutes les recherches enregistrées, planifications et créées par hello API Analytique de journal des actions doit être en minuscules.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Modification d’une planification
Utilisez la méthode de Put de hello avec une planification existante ID pour hello même enregistrée rechercher toomodify planifier.  corps de Hello de demande de hello doit inclure etag hello de planification de hello.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Suppression de planifications
Utilisez la méthode de suppression de hello avec un toodelete ID de planification une planification.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Actions
Une planification peut avoir plusieurs actions. Une action peut définir un ou plusieurs tooperform de processus tels que l’envoi d’un message électronique ou le démarrage d’un runbook, ou elle peut définir un seuil qui détermine quand des résultats d’une recherche hello correspondent à certains critères.  Certaines actions à la fois définirez afin que le processus de hello sont effectuées lorsque hello seuil est atteint.

Toutes les actions ont des propriétés de hello Bonjour tableau suivant.  Différents types d’alertes ont différentes propriétés supplémentaires qui sont décrites ci-dessous.

| Propriété | Description |
|:--- |:--- |
| Type |Type d’action de hello.  Actuellement, les valeurs possibles de hello sont alerte et Webhook. |
| Nom |Nom complet de l’alerte de hello. |
| Version |Hello version API utilisée.  Actuellement, il doit toujours être défini too1. |

### <a name="retrieving-actions"></a>Récupération des actions
Méthode tooretrieve d’obtenir hello d’utiliser toutes les actions pour une planification.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Hello d’utilisation Get (méthode) avec hello action ID tooretrieve une action particulière pour une planification.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Création ou modification des actions
Utilisez la méthode de Put de hello avec un ID d’action qui est unique toohello planification toocreate une nouvelle action.  Lorsque vous créez une action dans la console OMS hello, un GUID est pour le code d’action hello.

> [!NOTE]
> nom de Hello pour toutes les recherches enregistrées, planifications et créées par hello API Analytique de journal des actions doit être en minuscules.

Utiliser la méthode Put de hello avec un ID pour hello même enregistrée rechercher toomodify planifier des actions existant.  corps de Hello de demande de hello doit inclure etag hello de planification de hello.

format de demande Hello pour la création d’une nouvelle action varie selon le type d’action pour ces exemples sont fournis dans les sections hello ci-dessous.

### <a name="deleting-actions"></a>Suppression des actions
Utilisez la méthode de suppression de hello avec hello action ID toodelete une action.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Actions d’alerte
Une planification doit avoir une, et une seule, action d’alerte.  Actions d’alerte ont un ou plusieurs des sections hello Bonjour tableau suivant.  Chacune est décrite plus en détail ci-dessous.

| Section | Description |
|:--- |:--- |
| Seuil |Critères quand l’action de hello est exécuté. |
| EmailNotification |Envoyer des messages toomultiple destinataires. |
| Correction |Démarrer un runbook dans Azure Automation tooattempt toocorrect identifié le problème. |

#### <a name="thresholds"></a>Seuils
Une action d’alerte ne doit avoir qu’un seul seuil.  Lorsque des résultats d’une recherche enregistrée hello correspondent seuil hello dans une action associée à cette recherche, tous les autres processus dans cette action sont exécutés.  En outre, une action peut ne contenir qu’un seuil et être ainsi utilisable avec d’autres types d’actions ne comportant pas de seuils.

Seuils ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Operator |Opérateur de comparaison des seuils hello. <br> gt = supérieur à <br> lt = inférieur à |
| Valeur |Valeur de seuil de hello. |

Par exemple, considérez une requête d’événement avec Interval défini sur 15 minutes, QueryTimeSpan sur 30 minutes et Threshold sur une valeur supérieure à 10. Dans ce cas, les requêtes hello sont exécuté toutes les 15 minutes, et se déclenchera une alerte si elle a retourné les 10 événements qui ont été créés sur un intervalle de 30 minutes.

Voici un exemple de réponse pour une action comportant uniquement un seuil.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de seuil pour une planification.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Utilisez hello Put méthode avec une toomodify d’ID action existante une action de seuil pour une planification.  corps de Hello de demande de hello doit inclure etag hello d’action de hello.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Notification par courrier électronique
Envoient des Notifications par courrier électronique tooone de messagerie ou d’autres destinataires.  Elles incluent des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Recipients |Liste d’adresses de messagerie. |
| Objet |objet de Hello de message de salutation. |
| Pièce jointe |Les pièces jointes n’étant pas actuellement prises en charge, cette propriété est toujours définie sur « None ». |

Voici un exemple de réponse pour une action de notification par courrier électronique comportant un seuil.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de courrier électronique pour une planification.  Hello exemple suivant crée une notification par courrier électronique avec un seuil pour les messages hello sont envoyé lorsque les résultats de hello Hello recherche enregistrée dépassent le seuil de hello.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Utilisez hello Put méthode avec une toomodify d’ID action existante une action de courrier électronique pour une planification.  corps de Hello de demande de hello doit inclure etag hello d’action de hello.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Actions de correction
Corrections de démarrer un runbook dans Azure Automation qui tente de problème de hello toocorrect identifié par l’alerte de hello.  Vous devez créer un webhook pour runbook hello utilisé dans une action de mise à jour, puis spécifiez hello URI Bonjour WebhookUri propriété.  Lorsque vous créez cette action à l’aide de la console OMS de hello, un nouveau webhook est automatiquement créé pour hello runbook.

Des corrections incluent les propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| RunbookName |Nom du runbook de hello. Cela doit correspondre à un runbook publié dans le compte d’automatisation hello configuré Bonjour Solution Automation dans votre espace de travail OMS. |
| WebhookUri |URI de hello webhook. |
| Expiry |date d’expiration de Hello et l’heure de hello webhook.  Si hello webhook n’a pas un délai d’expiration, cela peut être une date future valide. |

Voici un exemple de réponse pour une action de correction comportant un seuil.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de mise à jour pour une planification.  Hello exemple suivant crée une mise à jour avec un seuil hello runbook est démarré lorsque les résultats de hello Hello recherche enregistrée dépassent le seuil de hello.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Utilisez hello Put méthode avec une toomodify d’ID action existante une action de mise à jour pour une planification.  corps de Hello de demande de hello doit inclure etag hello d’action de hello.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Exemple
Voici un exemple complet de toocreate une alerte par courrier électronique.  Cet exemple crée une planification avec une action qui contient un seuil et un e-mail.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Actions de webhook
Les actions Webhook démarrer un processus en appelant une URL et éventuellement en fournissant un toobe de charge utile envoyée.  Ils sont des actions tooRemediation similaires à ceci près qu’ils sont destinés à webhooks qui peut appeler des processus autres que les runbooks Azure Automation.  Elles fournissent également hello option supplémentaire permettant de fournir un processus à distance de charge utile toobe remis toohello.

Les actions Webhook n’ont pas d’un seuil, mais au lieu de cela doivent être ajoutées planification tooa qui a une action avec un seuil d’alerte.  Vous pouvez ajouter plusieurs actions Webhook qui seront toutes exécutées lorsque hello seuil est atteint.

Les actions Webhook incluent les propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| WebhookUri |objet de Hello de message de salutation. |
| CustomPayload |Charge utile personnalisée toobe envoyé toohello webhook.  format de Hello dépend de quelles webhook hello est attendu. |

Voici un exemple de réponse pour l’action webhook et une action d’alerte associée comportant un seuil.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Créer ou modifier une action de webhook
Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de webhook pour une planification.  Hello exemple suivant crée une action de Webhook et une action d’alerte avec un seuil afin que hello webhook est déclenchée lorsque les résultats de hello Hello recherche enregistrée dépassent le seuil de hello.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Utilisez hello Put méthode avec une toomodify d’ID action existante une action de webhook pour une planification.  corps de Hello de demande de hello doit inclure etag hello d’action de hello.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Étapes suivantes
* Hello d’utilisation [API REST des recherches de journaux tooperform](log-analytics-log-search-api.md) dans le journal Analytique.

