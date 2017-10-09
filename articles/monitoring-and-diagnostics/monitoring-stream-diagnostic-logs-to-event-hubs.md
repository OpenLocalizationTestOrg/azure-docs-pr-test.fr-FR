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
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="eb6b0-103">Flux de données des journaux de Diagnostic Azure tooan Namespace de concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="eb6b0-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="eb6b0-104">**[Les journaux de diagnostic Azure](monitoring-overview-of-diagnostic-logs.md)**  peut être transmis en continu près de l’option de « L’exportation tooEvent concentrateurs » intégrée hello dans hello portail application tooany en temps réel, ou en activant hello ID de règle de Bus de Service dans un paramètre de diagnostic via hello Azure PowerShell CLI applets de commande ou Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="eb6b0-105">Ce que vous pouvez faire avec les journaux de diagnostic et Event Hubs</span><span class="sxs-lookup"><span data-stu-id="eb6b0-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="eb6b0-106">Voici quelques méthodes que vous pouvez utiliser hello capacité de diffusion en continu pour les journaux de Diagnostic :</span><span class="sxs-lookup"><span data-stu-id="eb6b0-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="eb6b0-107">**Flux de données consigne les systèmes de journalisation et les données de télémétrie too3rd tiers** – au fil du temps, le concentrateurs d’événements de diffusion en continu deviennent hello mécanisme toopipe vos journaux de diagnostic dans les serveurs de SIEM toothird tiers et les solutions analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="eb6b0-108">**Afficher l’intégrité du service par diffusion en continu de « chemin réactif » données tooPowerBI** – concentrateurs d’événements à l’aide de flux Analytique et Power BI, vous pouvez facilement transformer vos données de diagnostic dans les informations en temps réel toonear sur vos services Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="eb6b0-109">[Cet article de la documentation permet de découvrir comment traiter les données avec le flux de données Analytique tooset des concentrateurs d’événements et utiliser Power BI comme sortie](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="eb6b0-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="eb6b0-110">Voici quelques conseils pour la configuration des journaux de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="eb6b0-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="eb6b0-111">Un concentrateur d’événements pour une catégorie de journaux de diagnostic est créé automatiquement lorsque vous activez option hello dans le portail de hello ou l’activer via PowerShell, donc le concentrateur d’événements tooselect hello dans hello espace de noms avec le nom de hello commence par **insights-**.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="eb6b0-112">Hello suivant le code SQL est un exemple de flux de données Analytique requête que vous pouvez utiliser tooparse toutes les données de journal hello dans la table de Power BI tooa :</span><span class="sxs-lookup"><span data-stu-id="eb6b0-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="eb6b0-113">**Générer une télémétrie personnalisée et la plateforme de journalisation** : Si vous disposez déjà d’une plateforme de télémétrie personnalisées ou sont simplement penser à la génération 1, hello hautement évolutive de publication / abonnement nature des concentrateurs d’événements vous permet de tooflexibly réception du diagnostic journaux.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="eb6b0-114">[Consultez le toousing de Dan Rosanova guide concentrateurs d’événements dans une plateforme de télémétrie à l’échelle mondiale ici](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="eb6b0-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="eb6b0-115">Activer la diffusion en continu des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="eb6b0-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="eb6b0-116">Vous pouvez activer la diffusion en continu des journaux de diagnostic par programme, via le portail de hello, ou à l’aide de hello [API REST de Azure analyse](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="eb6b0-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="eb6b0-117">Dans les deux cas, vous créez un paramètre de diagnostic dans lequel vous spécifiez un espace de noms de concentrateurs d’événements et catégories du journal hello et métriques toosend dans l’espace de noms toohello.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="eb6b0-118">Un concentrateur d’événements est créé dans l’espace de noms hello pour chaque catégorie de journal que vous activez.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="eb6b0-119">Une **catégorie de journal** de diagnostic est un type de journal qu’une ressource peut collecter.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="eb6b0-120">L’activation et la diffusion en continu de journaux de diagnostic à partir de ressources de calcul (par exemple, les machines virtuelles ou Service Fabric) [nécessitent des étapes de configuration différentes](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="eb6b0-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="eb6b0-121">Hello Service Bus ou concentrateurs d’événements espace de noms n’a pas toobe dans hello même abonnement en tant que ressource hello générant des journaux tant qu’utilisateur hello configure hello paramètre a des abonnements de tooboth accès RBAC appropriés.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="eb6b0-122">Flux de données des journaux de diagnostic à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="eb6b0-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="eb6b0-123">Dans le portail de hello, accédez tooAzure moniteur, puis cliquez sur **les paramètres de Diagnostic**</span><span class="sxs-lookup"><span data-stu-id="eb6b0-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Section Surveillance d’Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="eb6b0-125">Vous pouvez également filtrer la liste de hello par type de ressource ou le groupe de ressources, puis cliquez sur ressources hello pour laquelle vous aimeriez tooset un paramètre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="eb6b0-126">Si aucun paramètre n’existe sur la ressource hello que vous avez sélectionné, vous êtes invité à toocreate un paramètre.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="eb6b0-127">Cliquez sur « Activer les diagnostics ».</span><span class="sxs-lookup"><span data-stu-id="eb6b0-127">Click "Turn on diagnostics."</span></span>

   ![Ajouter le paramètre de diagnostic - aucun paramètre existant](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="eb6b0-129">S’il existe des paramètres existants sur les ressources hello, vous verrez une liste de paramètres déjà configuré sur cette ressource.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="eb6b0-130">Cliquez sur « Ajouter le paramètre de diagnostic ».</span><span class="sxs-lookup"><span data-stu-id="eb6b0-130">Click "Add diagnostic setting."</span></span>

   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="eb6b0-132">Donnez à votre définition d’un nom et la case hello pour **concentrateur d’événements de flux tooan**, puis sélectionnez un espace de noms de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="eb6b0-134">Hello espace de noms sélectionné sera où le concentrateur d’événements hello est créé (s’il s’agit de votre première diffusion en continu des journaux de diagnostic) ou transmis en continu trop (s’il existe déjà les ressources qui sont de diffusion en continu cet espace de noms de journal catégorie toothis), et définit la stratégie de hello hello autorisations dont dispose de mécanisme de diffusion en continu hello.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="eb6b0-135">Aujourd'hui, concentrateur d’événements tooan de diffusion en continu requiert écouter, envoyer et gérer les autorisations.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="eb6b0-136">Vous pouvez créer ou modifier des stratégies d’accès partagé un espace de noms concentrateurs d’événements dans le portail hello sous l’onglet configurer de hello pour votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="eb6b0-137">tooupdate un de ces paramètres de diagnostic, les clients hello doivent autorisé hello ListKey sur une règle d’autorisation hello concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="eb6b0-138">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-138">Click **Save**.</span></span>

<span data-ttu-id="eb6b0-139">Après quelques instants, hello nouveau paramètre s’affiche dans la liste des paramètres pour cette ressource, et les journaux de diagnostic sont transmis en continu compte de stockage toothat dès que les nouvelles données d’événement sont générées.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="eb6b0-140">Via les applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb6b0-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="eb6b0-141">tooenable de diffusion en continu via hello [applets de commande PowerShell Azure](insights-powershell-samples.md), vous pouvez utiliser hello `Set-AzureRmDiagnosticSetting` applet de commande avec ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="eb6b0-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="eb6b0-142">Hello ID de règle de Bus de Service est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`, par exemple, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="eb6b0-143">Via l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="eb6b0-143">Via Azure CLI</span></span>
<span data-ttu-id="eb6b0-144">tooenable de diffusion en continu via hello [CLI d’Azure](insights-cli-samples.md), vous pouvez utiliser hello `insights diagnostic set` commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb6b0-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="eb6b0-145">Utilisez hello même format pour l’ID de règle de Bus de Service, comme expliqué pour hello PowerShell Cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="eb6b0-146">Comment consommer des données de journal hello de concentrateurs d’événements ?</span><span class="sxs-lookup"><span data-stu-id="eb6b0-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="eb6b0-147">Voici des exemples de données de sortie provenant d’Event Hubs :</span><span class="sxs-lookup"><span data-stu-id="eb6b0-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="eb6b0-148">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="eb6b0-148">Element Name</span></span> | <span data-ttu-id="eb6b0-149">Description</span><span class="sxs-lookup"><span data-stu-id="eb6b0-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb6b0-150">records</span><span class="sxs-lookup"><span data-stu-id="eb6b0-150">records</span></span> |<span data-ttu-id="eb6b0-151">Un tableau regroupant tous les événements de journal de cette charge utile.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="eb6b0-152">time</span><span class="sxs-lookup"><span data-stu-id="eb6b0-152">time</span></span> |<span data-ttu-id="eb6b0-153">Heure à laquelle hello événement s’est produit.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="eb6b0-154">category</span><span class="sxs-lookup"><span data-stu-id="eb6b0-154">category</span></span> |<span data-ttu-id="eb6b0-155">La catégorie de journal associée à cet événement.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-155">Log category for this event.</span></span> |
| <span data-ttu-id="eb6b0-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="eb6b0-156">resourceId</span></span> |<span data-ttu-id="eb6b0-157">ID de ressource de la ressource hello qui a généré cet événement.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="eb6b0-158">operationName</span><span class="sxs-lookup"><span data-stu-id="eb6b0-158">operationName</span></span> |<span data-ttu-id="eb6b0-159">Nom de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-159">Name of hello operation.</span></span> |
| <span data-ttu-id="eb6b0-160">level</span><span class="sxs-lookup"><span data-stu-id="eb6b0-160">level</span></span> |<span data-ttu-id="eb6b0-161">facultatif.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-161">Optional.</span></span> <span data-ttu-id="eb6b0-162">Indique le niveau de l’événement journal hello.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="eb6b0-163">properties</span><span class="sxs-lookup"><span data-stu-id="eb6b0-163">properties</span></span> |<span data-ttu-id="eb6b0-164">Propriétés d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-164">Properties of hello event.</span></span> |

<span data-ttu-id="eb6b0-165">Vous pouvez afficher une liste de tous les fournisseurs de ressources qui prennent en charge la diffusion en continu de concentrateurs de tooEvent [ici](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="eb6b0-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="eb6b0-166">Diffusion de données à partir des ressources de calcul</span><span class="sxs-lookup"><span data-stu-id="eb6b0-166">Stream data from Compute resources</span></span>
<span data-ttu-id="eb6b0-167">Vous pouvez également transmettre en continu des journaux de diagnostic à partir des ressources de calcul à l’aide de l’agent de Diagnostics Windows Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="eb6b0-168">[Consultez l’article](../event-hubs/event-hubs-streaming-azure-diags-data.md) sur la manière de tooset cet accès.</span><span class="sxs-lookup"><span data-stu-id="eb6b0-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb6b0-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb6b0-169">Next steps</span></span>
* [<span data-ttu-id="eb6b0-170">En savoir plus sur les journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="eb6b0-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="eb6b0-171">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="eb6b0-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

