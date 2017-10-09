---
title: tooalerts aaaResponses dans Analytique des journaux OMS | Documents Microsoft
description: "Alertes dans le journal Analytique identifier des informations importantes dans votre référentiel OMS et peuvent proactive vous avertir des problèmes ou appeler des actions tooattempt toocorrect les.  Cet article décrit comment toocreate une règle d’alerte et des actions différentes informations hello qu’ils peuvent prendre."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Ajouter des règles de tooalert d’actions dans le journal Analytique
Lorsqu’un [alerte est créée dans le journal Analytique](log-analytics-alerts.md), vous pouvez hello [une règle d’alerte hello configuration](log-analytics-alerts.md) tooperform une ou plusieurs actions.  Cet article décrit hello différentes actions qui sont disponibles et les détails sur la configuration de chaque type.

| Action | Description |
|:--|:--|
| [E-mail](#email-actions) | Envoyer un message électronique avec les détails de hello de tooone d’alerte hello ou autres destinataires. |
| [Webhook](#webhook-actions) | Appelez un processus externe par le biais d’une simple requête HTTP POST. |
| [Runbook](#runbook-actions) | Démarrez un runbook dans Azure Automation. |


## <a name="email-actions"></a>Actions de messagerie
Les actions par courrier électronique envoient un e-mail avec les détails de hello de tooone d’alerte hello ou autres destinataires.  Vous pouvez spécifier le sujet hello de messagerie de hello, mais son contenu est un format standard construit par Analytique de journal.  Il inclut des informations de synthèse, telles que nom de hello d’alerte de hello dans toodetails Ajout d’enregistrements tooten retournée par la recherche de journal hello.  Il inclut également une recherche de journal de liaison tooa dans Analytique de journal qui retournera le jeu complet de hello d’enregistrements à partir de cette requête.   expéditeur Hello de messagerie de hello est *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* . 

Les actions de messagerie nécessitent propriétés hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Objet |L’objet par courrier électronique hello.  Vous ne pouvez pas modifier le corps hello de messagerie de hello. |
| Destinataires |Adresses de tous les destinataires de l’e-mail.  Si vous spécifiez plusieurs adresses, puis les adresses hello séparé par un point-virgule ( ;). |


## <a name="webhook-actions"></a>Actions de webhook

Les actions Webhook permettent tooinvoke un processus externe via une demande HTTP POST unique.  service Hello appelé doit prendre en charge des webhooks et déterminer la façon dont il va utiliser une charge utile qu’il reçoit.  Vous pouvez également appeler une API REST qui ne prennent en charge spécifiquement webhooks tant que la demande de hello est dans un format que hello que comprend des API.  Exemples d’utilisation d’un webhook dans l’alerte de tooan réponse envoient un message [Slack](http://slack.com) ou la création d’un incident dans [PagerDuty](http://pagerduty.com/).  Une procédure pas à pas complète de la création d’une règle d’alerte avec une marge de toocall webhook est disponible à l’adresse [Webhooks dans les alertes d’Analytique de journal](log-analytics-alerts-webhooks.md).

Les actions Webhook requièrent des propriétés hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| URL du webhook |URL de Hello de hello webhook. |
| Charge utile JSON personnalisée |Toosend de charge utile personnalisée avec hello webhook.  Voir les détails ci-dessous. |


Webhooks inclure une URL et une charge utile au format JSON qui sont des données hello envoyé toohello des service externe.  Par défaut, la charge utile de hello inclut les valeurs hello Bonjour tableau suivant.  Vous pouvez choisir tooreplace cette charge utile avec un personnalisé de votre choix.  Dans ce cas vous pouvez utiliser des variables de hello dans la table de hello pour chacun des hello paramètres tooinclude leur valeur dans votre charge utile personnalisée.

| Paramètre | Variable | Description |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Nom de règle d’alerte hello. |
| AlertThresholdOperator |#thresholdoperator |Opérateur de seuil pour la règle d’alerte hello.  *Supérieur à* ou *Inférieur à*. |
| AlertThresholdValue |#thresholdvalue |Valeur de seuil pour la règle d’alerte hello. |
| LinkToSearchResults |#linktosearchresults |Lier la recherche de journal d’Analytique tooLog qui retourne des enregistrements de hello dans la requête hello créé hello alerte. |
| ResultCount |#searchresultcount |Nombre d’enregistrements dans les résultats de recherche hello. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Heure de fin de la requête hello au format UTC. |
| SearchIntervalInSeconds |#searchinterval |Fenêtre de temps pour la règle d’alerte hello. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Heure de début de requête de hello au format UTC. |
| SearchQuery |#searchquery |Requête de recherche de journal utilisé par la règle d’alerte hello. |
| SearchResults |Voir ci-dessous |Enregistrements retournés par la requête hello au format JSON.  Toohello limitée 5 000 premiers enregistrements. |
| WorkspaceID |#workspaceid |ID de votre espace de travail OMS. |

Par exemple, vous pouvez spécifier hello suivant charge utile personnalisée qui inclut un paramètre unique appelé *texte*.  service de Hello ce webhook appelle serait être attendu de ce paramètre.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Cet exemple de charge utile résolvait toosomething comme hello suivant lorsque envoyé toohello webhook.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

tooinclude les résultats de recherche dans une charge utile personnalisée, ajoutez hello suivant la ligne comme une propriété de niveau supérieur dans la charge utile json de hello.  

    "IncludeSearchResults":true

Par exemple, toocreate une charge utile personnalisée qui inclut le nom de l’alerte hello et de résultats de la recherche hello, vous pouvez utiliser hello suivant. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Vous suivez les étapes d’un exemple complet de la création d’un service externe à une règle d’alerte avec un toostart webhook [créer une action de l’alerte webhook dans Analytique des journaux OMS toosend message tooSlack](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Actions de runbook
Les actions de runbook démarrent un runbook dans Azure Automation.  Dans commande toouse ce type d’action, vous devez avoir hello [solution Automation](log-analytics-add-solutions.md) installé et configuré dans votre espace de travail OMS.  Vous pouvez sélectionner à partir des runbooks hello dans compte automation hello que vous avez configuré dans hello solution Automation.

Actions de runbooks requièrent des propriétés hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:---|
| Runbook | Runbook que vous souhaitez toostart lorsqu’une alerte est créée. |
| Exécuter sur | Spécifiez **Azure** runbook de hello toorun dans le cloud de hello.  Spécifiez **worker hybride** runbook de hello toorun sur un agent avec [Runbook Worker hybride](../automation/automation-hybrid-runbook-worker.md ) installé.  |

Actions de runbooks démarrer à l’aide de runbook hello un [webhook](../automation/automation-webhooks.md).  Lorsque vous créez une règle d’alerte hello, il crée automatiquement un nouveau webhook hello runbook avec le nom de hello **OMS alerte correction** suivi d’un GUID.  

Vous ne pouvez pas remplir tous les paramètres du runbook de hello directement, mais hello [$WebhookData paramètre](../automation/automation-webhooks.md) inclura des détails hello d’alerte hello, y compris les hello les résultats de recherche de journal hello qui l’a créée.  Hello runbook devez toodefine **$WebhookData** en tant que paramètre pour qu’il tooaccess hello des propriétés d’alerte de hello.  Hello données d’alerte ne sont disponibles au format json dans une propriété unique appelée **SearchResults** Bonjour **RequestBody** propriété du **$WebhookData**.  Cela aura des propriétés de hello en hello tableau suivant.

| Nœud | Description |
|:--- |:--- |
| id |Chemin d’accès et le GUID de la recherche de hello. |
| __metadata |Informations sur hello alerte notamment hello nombre d’enregistrements et l’état hello des résultats de recherche. |
| value |Entrée distincte pour chaque enregistrement dans les résultats de recherche hello.  Détails de Hello d’entrée de hello seront correspondent aux propriétés de hello et les valeurs de l’enregistrement de hello. |

Par exemple, hello runbook suivant serait extraire des enregistrements hello retournées par la recherche de journal hello et attribuer des propriétés différentes en fonction de type hello de chaque enregistrement.  Notez que runbook hello commence en convertissant **RequestBody** à partir de json afin qu’elles puissent être utilisés en tant qu’objet dans PowerShell.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Étapes suivantes
- Effectuez une procédure pas à pas pour [configurer un webhook](log-analytics-alerts-webhooks.md) avec une règle d’alerte.  
- Découvrez comment toowrite [runbooks dans Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate les problèmes identifiés par des alertes.
