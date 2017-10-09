---
title: "aaaStream les journaux de Diagnostic Azure tooan Namespace de concentrateurs d’événements | Documents Microsoft"
description: "Découvrez comment toostream Azure diagnostic consigne espace de noms tooan concentrateurs d’événements."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Flux de données des journaux de Diagnostic Azure tooan Namespace de concentrateurs d’événements
**[Les journaux de diagnostic Azure](monitoring-overview-of-diagnostic-logs.md)**  peut être transmis en continu près de l’option de « L’exportation tooEvent concentrateurs » intégrée hello dans hello portail application tooany en temps réel, ou en activant hello ID de règle de Bus de Service dans un paramètre de diagnostic via hello Azure PowerShell CLI applets de commande ou Azure.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Ce que vous pouvez faire avec les journaux de diagnostic et Event Hubs
Voici quelques méthodes que vous pouvez utiliser hello capacité de diffusion en continu pour les journaux de Diagnostic :

* **Flux de données consigne les systèmes de journalisation et les données de télémétrie too3rd tiers** – au fil du temps, le concentrateurs d’événements de diffusion en continu deviennent hello mécanisme toopipe vos journaux de diagnostic dans les serveurs de SIEM toothird tiers et les solutions analytique de journal.
* **Afficher l’intégrité du service par diffusion en continu de « chemin réactif » données tooPowerBI** – concentrateurs d’événements à l’aide de flux Analytique et Power BI, vous pouvez facilement transformer vos données de diagnostic dans les informations en temps réel toonear sur vos services Azure. [Cet article de la documentation permet de découvrir comment traiter les données avec le flux de données Analytique tooset des concentrateurs d’événements et utiliser Power BI comme sortie](../stream-analytics/stream-analytics-power-bi-dashboard.md). Voici quelques conseils pour la configuration des journaux de diagnostic :
  
  * Un concentrateur d’événements pour une catégorie de journaux de diagnostic est créé automatiquement lorsque vous activez option hello dans le portail de hello ou l’activer via PowerShell, donc le concentrateur d’événements tooselect hello dans hello espace de noms avec le nom de hello commence par **insights-**.
  * Hello suivant le code SQL est un exemple de flux de données Analytique requête que vous pouvez utiliser tooparse toutes les données de journal hello dans la table de Power BI tooa :

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Générer une télémétrie personnalisée et la plateforme de journalisation** : Si vous disposez déjà d’une plateforme de télémétrie personnalisées ou sont simplement penser à la génération 1, hello hautement évolutive de publication / abonnement nature des concentrateurs d’événements vous permet de tooflexibly réception du diagnostic journaux. [Consultez le toousing de Dan Rosanova guide concentrateurs d’événements dans une plateforme de télémétrie à l’échelle mondiale ici](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Activer la diffusion en continu des journaux de diagnostic
Vous pouvez activer la diffusion en continu des journaux de diagnostic par programme, via le portail de hello, ou à l’aide de hello [API REST de Azure analyse](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). Dans les deux cas, vous créez un paramètre de diagnostic dans lequel vous spécifiez un espace de noms de concentrateurs d’événements et catégories du journal hello et métriques toosend dans l’espace de noms toohello. Un concentrateur d’événements est créé dans l’espace de noms hello pour chaque catégorie de journal que vous activez. Une **catégorie de journal** de diagnostic est un type de journal qu’une ressource peut collecter.

> [!WARNING]
> L’activation et la diffusion en continu de journaux de diagnostic à partir de ressources de calcul (par exemple, les machines virtuelles ou Service Fabric) [nécessitent des étapes de configuration différentes](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Hello Service Bus ou concentrateurs d’événements espace de noms n’a pas toobe dans hello même abonnement en tant que ressource hello générant des journaux tant qu’utilisateur hello configure hello paramètre a des abonnements de tooboth accès RBAC appropriés.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Flux de données des journaux de diagnostic à l’aide du portail de hello
1. Dans le portail de hello, accédez tooAzure moniteur, puis cliquez sur **les paramètres de Diagnostic**

    ![Section Surveillance d’Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Vous pouvez également filtrer la liste de hello par type de ressource ou le groupe de ressources, puis cliquez sur ressources hello pour laquelle vous aimeriez tooset un paramètre de diagnostic.

3. Si aucun paramètre n’existe sur la ressource hello que vous avez sélectionné, vous êtes invité à toocreate un paramètre. Cliquez sur « Activer les diagnostics ».

   ![Ajouter le paramètre de diagnostic - aucun paramètre existant](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   S’il existe des paramètres existants sur les ressources hello, vous verrez une liste de paramètres déjà configuré sur cette ressource. Cliquez sur « Ajouter le paramètre de diagnostic ».

   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Donnez à votre définition d’un nom et la case hello pour **concentrateur d’événements de flux tooan**, puis sélectionnez un espace de noms de concentrateurs d’événements.
   
   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Hello espace de noms sélectionné sera où le concentrateur d’événements hello est créé (s’il s’agit de votre première diffusion en continu des journaux de diagnostic) ou transmis en continu trop (s’il existe déjà les ressources qui sont de diffusion en continu cet espace de noms de journal catégorie toothis), et définit la stratégie de hello hello autorisations dont dispose de mécanisme de diffusion en continu hello. Aujourd'hui, concentrateur d’événements tooan de diffusion en continu requiert écouter, envoyer et gérer les autorisations. Vous pouvez créer ou modifier des stratégies d’accès partagé un espace de noms concentrateurs d’événements dans le portail hello sous l’onglet configurer de hello pour votre espace de noms. tooupdate un de ces paramètres de diagnostic, les clients hello doivent autorisé hello ListKey sur une règle d’autorisation hello concentrateurs d’événements.

4. Cliquez sur **Enregistrer**.

Après quelques instants, hello nouveau paramètre s’affiche dans la liste des paramètres pour cette ressource, et les journaux de diagnostic sont transmis en continu compte de stockage toothat dès que les nouvelles données d’événement sont générées.

### <a name="via-powershell-cmdlets"></a>Via les applets de commande PowerShell
tooenable de diffusion en continu via hello [applets de commande PowerShell Azure](insights-powershell-samples.md), vous pouvez utiliser hello `Set-AzureRmDiagnosticSetting` applet de commande avec ces paramètres :

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Hello ID de règle de Bus de Service est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`, par exemple, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>Via l’interface de ligne de commande Azure
tooenable de diffusion en continu via hello [CLI d’Azure](insights-cli-samples.md), vous pouvez utiliser hello `insights diagnostic set` commande comme suit :

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Utilisez hello même format pour l’ID de règle de Bus de Service, comme expliqué pour hello PowerShell Cmdlet.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Comment consommer des données de journal hello de concentrateurs d’événements ?
Voici des exemples de données de sortie provenant d’Event Hubs :

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Nom de l’élément | Description |
| --- | --- |
| records |Un tableau regroupant tous les événements de journal de cette charge utile. |
| time |Heure à laquelle hello événement s’est produit. |
| category |La catégorie de journal associée à cet événement. |
| resourceId |ID de ressource de la ressource hello qui a généré cet événement. |
| operationName |Nom de l’opération de hello. |
| level |facultatif. Indique le niveau de l’événement journal hello. |
| properties |Propriétés d’événement de hello. |

Vous pouvez afficher une liste de tous les fournisseurs de ressources qui prennent en charge la diffusion en continu de concentrateurs de tooEvent [ici](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Diffusion de données à partir des ressources de calcul
Vous pouvez également transmettre en continu des journaux de diagnostic à partir des ressources de calcul à l’aide de l’agent de Diagnostics Windows Azure hello. [Consultez l’article](../event-hubs/event-hubs-streaming-azure-diags-data.md) sur la manière de tooset cet accès.

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les journaux de diagnostic Azure](monitoring-overview-of-diagnostic-logs.md)
* [Prise en main des hubs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

