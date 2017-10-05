---
title: Diffuser en continu les journaux de diagnostic Azure vers un espace de noms Event Hubs | Microsoft Docs
description: "Découvrez comment diffuser en continu les journaux de diagnostic Azure vers un espace de noms Event Hubs."
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
ms.openlocfilehash: 01ba8ddfcf90e1368ac147296fd180f99420d96f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hubs-namespace"></a><span data-ttu-id="0eaac-103">Diffuser en continu les journaux de diagnostic Azure vers un espace de noms Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0eaac-103">Stream Azure Diagnostic Logs to an Event Hubs Namespace</span></span>
<span data-ttu-id="0eaac-104">Les **[journaux de diagnostic Azure](monitoring-overview-of-diagnostic-logs.md)** peuvent être diffusés quasiment en temps réel sur n’importe quelle application à l’aide de l’option « Exporter vers Event Hubs » intégrée au portail, ou en activant l’identifiant de règle Service Bus dans un paramètre de diagnostic via les applets de commande Azure PowerShell ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="0eaac-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule ID in a diagnostic setting via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="0eaac-105">Ce que vous pouvez faire avec les journaux de diagnostic et Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0eaac-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="0eaac-106">Voici quelques façons d’utiliser la fonctionnalité de diffusion en continu pour les journaux de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="0eaac-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="0eaac-107">**Diffuser en continu des journaux sur des systèmes de journalisation et de télémétrie tiers** : au fil du temps, la diffusion en continu sur Event Hubs deviendra le mécanisme de diffusion de vos journaux de diagnostic vers les SIEM et les solutions d’analyse de journaux tiers.</span><span class="sxs-lookup"><span data-stu-id="0eaac-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your diagnostic logs in to third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="0eaac-108">**Afficher l’état d’intégrité du service en diffusant des données de chemin réactif vers PowerBI** : en utilisant Event Hubs, Stream Analytics et PowerBI, vous pouvez facilement transformer vos données de diagnostic en informations en temps réel sur vos services Azure.</span><span class="sxs-lookup"><span data-stu-id="0eaac-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in to near real-time insights on your Azure services.</span></span> <span data-ttu-id="0eaac-109">[Cette documentation vous explique comment configurer un client Event Hubs, traiter les données avec Stream Analytics et utiliser PowerBI comme sortie](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="0eaac-109">[This documentation article gives a great overview of how to set up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="0eaac-110">Voici quelques conseils pour la configuration des journaux de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="0eaac-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="0eaac-111">Un hub d’événements est automatiquement créé pour une catégorie de journaux de diagnostic lorsque vous activez l’option dans le portail ou par le biais de PowerShell. Sélectionnez le hub d’événements dans l’espace de noms dont le nom commence par **insights-**.</span><span class="sxs-lookup"><span data-stu-id="0eaac-111">An event hub for a category of diagnostic logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the event hub in the namespace with the name that starts with **insights-**.</span></span>
  * <span data-ttu-id="0eaac-112">Le code SQL suivant est un exemple de requête Stream Analytics que vous pouvez utiliser pour analyser toutes les données de journal dans une table PowerBI :</span><span class="sxs-lookup"><span data-stu-id="0eaac-112">The following SQL code is a sample Stream Analytics query that you can use to parse all the log data in to a PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="0eaac-113">**Créer une plateforme de journalisation et de télémétrie personnalisée** : si vous disposez déjà d’une plateforme de télémétrie personnalisée, ou si vous envisagez d’en créer une, la nature hautement évolutive de publication et d’abonnement d’Event Hubs vous permet d’intégrer avec souplesse les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="0eaac-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="0eaac-114">[Consultez ici le guide de Dan Rosanova sur l’utilisation d’Event Hubs dans une plateforme de télémétrie à échelle mondiale.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)</span><span class="sxs-lookup"><span data-stu-id="0eaac-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="0eaac-115">Activer la diffusion en continu des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="0eaac-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="0eaac-116">Vous pouvez activer la diffusion en continu des journaux de diagnostic par programme, via le portail ou à l’aide des [API REST Azure Monitor](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="0eaac-116">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="0eaac-117">Dans tous les cas, vous créez un paramètre de diagnostic dans lequel vous spécifiez un espace de noms Event Hubs et les catégories de journal et les indicateurs de performance que vous voulez envoyer dans l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="0eaac-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and the log categories and metrics you want to send in to the namespace.</span></span> <span data-ttu-id="0eaac-118">Un hub d’événements est créé dans l’espace de noms pour chaque catégorie de journal que vous activez.</span><span class="sxs-lookup"><span data-stu-id="0eaac-118">An event hub is created in the namespace for each log category you enable.</span></span> <span data-ttu-id="0eaac-119">Une **catégorie de journal** de diagnostic est un type de journal qu’une ressource peut collecter.</span><span class="sxs-lookup"><span data-stu-id="0eaac-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="0eaac-120">L’activation et la diffusion en continu de journaux de diagnostic à partir de ressources de calcul (par exemple, les machines virtuelles ou Service Fabric) [nécessitent des étapes de configuration différentes](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="0eaac-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="0eaac-121">Il n’est pas nécessaire que l’espace de noms Service Bus ou Event Hubs se trouve dans le même abonnement que la ressource générant des journaux, à condition que l’utilisateur configurant le paramètre ait un accès RBAC approprié aux deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="0eaac-121">The Service Bus or Event Hubs namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-the-portal"></a><span data-ttu-id="0eaac-122">Diffuser en continu les journaux de diagnostic à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="0eaac-122">Stream diagnostic logs using the portal</span></span>
1. <span data-ttu-id="0eaac-123">Dans le portail, accédez à Azure Monitor, puis cliquez sur **Paramètres de diagnostic**</span><span class="sxs-lookup"><span data-stu-id="0eaac-123">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Section Surveillance d’Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="0eaac-125">Vous pouvez également filtrer la liste par type ou groupe de ressources, puis cliquez sur la ressource pour laquelle vous souhaitez définir un paramètre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="0eaac-125">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="0eaac-126">S’il n’existe aucun paramètre sur la ressource que vous avez sélectionnée, vous êtes invité à créer un paramètre.</span><span class="sxs-lookup"><span data-stu-id="0eaac-126">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="0eaac-127">Cliquez sur « Activer les diagnostics ».</span><span class="sxs-lookup"><span data-stu-id="0eaac-127">Click "Turn on diagnostics."</span></span>

   ![Ajouter le paramètre de diagnostic - aucun paramètre existant](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="0eaac-129">S’il existe des paramètres existants sur la ressource, vous verrez une liste de paramètres déjà configurés sur cette ressource.</span><span class="sxs-lookup"><span data-stu-id="0eaac-129">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="0eaac-130">Cliquez sur « Ajouter le paramètre de diagnostic ».</span><span class="sxs-lookup"><span data-stu-id="0eaac-130">Click "Add diagnostic setting."</span></span>

   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="0eaac-132">Donnez un nom à votre définition et cochez la case **Diffuser en continu vers un hub d’événements**, puis sélectionnez un espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0eaac-132">Give your setting a name and check the box for **Stream to an event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="0eaac-134">L’espace de noms sélectionné sera l’espace où le hub d’événements sera créé (si c’est la première fois que vous diffusez en continu des journaux de diagnostic) ou vers lequel le hub d’événements diffusera les journaux (si des ressources diffusent déjà cette catégorie de journal vers cet espace de noms). La stratégie définit les autorisations dont dispose le mécanisme de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="0eaac-134">The namespace selected will be where the event hub is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="0eaac-135">À l’heure actuelle, la diffusion vers un hub d’événements requiert des autorisations de gestion, d’envoi et d’écoute.</span><span class="sxs-lookup"><span data-stu-id="0eaac-135">Today, streaming to an event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="0eaac-136">Vous pouvez créer ou modifier les stratégies d’accès partagé de l’espace de noms Event Hubs dans le portail sous l’onglet Configurer pour votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="0eaac-136">You can create or modify Event Hubs namespace shared access policies in the portal under the Configure tab for your namespace.</span></span> <span data-ttu-id="0eaac-137">Pour mettre à jour l’un de ces paramètres de diagnostic, le client doit avoir l’autorisation ListKey sur la règle d’autorisation Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0eaac-137">To update one of these diagnostic settings, the client must have the ListKey permission on the Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="0eaac-138">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0eaac-138">Click **Save**.</span></span>

<span data-ttu-id="0eaac-139">Après quelques instants, le nouveau paramètre apparaît dans la liste des paramètres de cette ressource, et les journaux de diagnostic sont diffusés en continu dans ce compte de stockage dès que de nouvelles données d’événement sont générées.</span><span class="sxs-lookup"><span data-stu-id="0eaac-139">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="0eaac-140">Via les applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="0eaac-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="0eaac-141">Pour activer la diffusion en continu via les [applets de commande Azure PowerShell](insights-powershell-samples.md), vous pouvez utiliser l’applet de commande `Set-AzureRmDiagnosticSetting` avec ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="0eaac-141">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="0eaac-142">L’ID de règle Service Bus est une chaîne au format `{Service Bus resource ID}/authorizationrules/{key name}`, par exemple, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="0eaac-142">The Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="0eaac-143">Via l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="0eaac-143">Via Azure CLI</span></span>
<span data-ttu-id="0eaac-144">Pour activer la diffusion en continu via [l’interface de ligne de commande Azure](insights-cli-samples.md), vous pouvez utiliser la commande `insights diagnostic set` comme suit :</span><span class="sxs-lookup"><span data-stu-id="0eaac-144">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="0eaac-145">Utilisez le même format pour l’ID de règle Service Bus, comme expliqué pour l’applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eaac-145">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="0eaac-146">Comment utiliser les données de journal d’Event Hubs ?</span><span class="sxs-lookup"><span data-stu-id="0eaac-146">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="0eaac-147">Voici des exemples de données de sortie provenant d’Event Hubs :</span><span class="sxs-lookup"><span data-stu-id="0eaac-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="0eaac-148">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="0eaac-148">Element Name</span></span> | <span data-ttu-id="0eaac-149">Description</span><span class="sxs-lookup"><span data-stu-id="0eaac-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0eaac-150">records</span><span class="sxs-lookup"><span data-stu-id="0eaac-150">records</span></span> |<span data-ttu-id="0eaac-151">Un tableau regroupant tous les événements de journal de cette charge utile.</span><span class="sxs-lookup"><span data-stu-id="0eaac-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="0eaac-152">time</span><span class="sxs-lookup"><span data-stu-id="0eaac-152">time</span></span> |<span data-ttu-id="0eaac-153">L’heure à laquelle l’événement s’est produit.</span><span class="sxs-lookup"><span data-stu-id="0eaac-153">Time at which the event occurred.</span></span> |
| <span data-ttu-id="0eaac-154">category</span><span class="sxs-lookup"><span data-stu-id="0eaac-154">category</span></span> |<span data-ttu-id="0eaac-155">La catégorie de journal associée à cet événement.</span><span class="sxs-lookup"><span data-stu-id="0eaac-155">Log category for this event.</span></span> |
| <span data-ttu-id="0eaac-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="0eaac-156">resourceId</span></span> |<span data-ttu-id="0eaac-157">L’ID de la ressource qui a généré cet événement.</span><span class="sxs-lookup"><span data-stu-id="0eaac-157">Resource ID of the resource that generated this event.</span></span> |
| <span data-ttu-id="0eaac-158">operationName</span><span class="sxs-lookup"><span data-stu-id="0eaac-158">operationName</span></span> |<span data-ttu-id="0eaac-159">Le nom de l’opération.</span><span class="sxs-lookup"><span data-stu-id="0eaac-159">Name of the operation.</span></span> |
| <span data-ttu-id="0eaac-160">level</span><span class="sxs-lookup"><span data-stu-id="0eaac-160">level</span></span> |<span data-ttu-id="0eaac-161">facultatif.</span><span class="sxs-lookup"><span data-stu-id="0eaac-161">Optional.</span></span> <span data-ttu-id="0eaac-162">Indique le niveau de l’événement de journal.</span><span class="sxs-lookup"><span data-stu-id="0eaac-162">Indicates the log event level.</span></span> |
| <span data-ttu-id="0eaac-163">properties</span><span class="sxs-lookup"><span data-stu-id="0eaac-163">properties</span></span> |<span data-ttu-id="0eaac-164">Les propriétés de l’événement.</span><span class="sxs-lookup"><span data-stu-id="0eaac-164">Properties of the event.</span></span> |

<span data-ttu-id="0eaac-165">Une liste de tous les fournisseurs de ressources qui prennent en charge la diffusion en continu vers Event Hubs est disponible [ici](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="0eaac-165">You can view a list of all resource providers that support streaming to Event Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="0eaac-166">Diffusion de données à partir des ressources de calcul</span><span class="sxs-lookup"><span data-stu-id="0eaac-166">Stream data from Compute resources</span></span>
<span data-ttu-id="0eaac-167">Vous pouvez également diffuser en continu des journaux de diagnostic à partir des ressources de calcul à l’aide de l’agent Windows Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="0eaac-167">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="0eaac-168">[Consultez cet article](../event-hubs/event-hubs-streaming-azure-diags-data.md) pour découvrir comment configurer cela.</span><span class="sxs-lookup"><span data-stu-id="0eaac-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eaac-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0eaac-169">Next steps</span></span>
* [<span data-ttu-id="0eaac-170">En savoir plus sur les journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="0eaac-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="0eaac-171">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="0eaac-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

