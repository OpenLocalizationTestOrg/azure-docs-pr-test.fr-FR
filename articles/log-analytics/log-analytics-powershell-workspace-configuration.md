---
title: aaaUse PowerShell tooCreate et configurer un espace de travail Analytique de journal | Documents Microsoft
description: "Log Analytics utilise des données des serveurs dans votre infrastructure locale ou dans le cloud. Vous pouvez collecter des données de la machine à partir du stockage Azure lorsqu’elles sont générées par les diagnostics Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="4d3f0-104">Gérer Log Analytics à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d3f0-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="4d3f0-105">Vous pouvez utiliser hello [applets de commande PowerShell Analytique de journal](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform diverses fonctions dans Analytique de journal à partir d’une ligne de commande ou dans le cadre d’un script.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="4d3f0-106">Voici quelques exemples de tâches hello que vous pouvez effectuer avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="4d3f0-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="4d3f0-107">Créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="4d3f0-107">Create a workspace</span></span>
* <span data-ttu-id="4d3f0-108">Ajouter ou supprimer une solution</span><span class="sxs-lookup"><span data-stu-id="4d3f0-108">Add or remove a solution</span></span>
* <span data-ttu-id="4d3f0-109">Importer et exporter des recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="4d3f0-109">Import and export saved searches</span></span>
* <span data-ttu-id="4d3f0-110">Créer un groupe d’ordinateurs</span><span class="sxs-lookup"><span data-stu-id="4d3f0-110">Create a computer group</span></span>
* <span data-ttu-id="4d3f0-111">Activer la collecte de journaux IIS à partir d’ordinateurs avec l’agent Windows hello installé</span><span class="sxs-lookup"><span data-stu-id="4d3f0-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="4d3f0-112">Collecter les compteurs de performances d’ordinateurs Linux et Windows</span><span class="sxs-lookup"><span data-stu-id="4d3f0-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="4d3f0-113">Collecter les événements de Syslog sur des ordinateurs Linux</span><span class="sxs-lookup"><span data-stu-id="4d3f0-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="4d3f0-114">Collecter les événements des journaux des événements Windows</span><span class="sxs-lookup"><span data-stu-id="4d3f0-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="4d3f0-115">Collecter des journaux des événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="4d3f0-115">Collect custom event logs</span></span>
* <span data-ttu-id="4d3f0-116">Ajouter hello journal analytique agent tooan machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="4d3f0-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="4d3f0-117">Configurer le journal analytique tooindex collectées à l’aide des diagnostics Windows Azure</span><span class="sxs-lookup"><span data-stu-id="4d3f0-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="4d3f0-118">Cet article fournit deux exemples de code qui illustrent les fonctions hello que vous pouvez effectuer à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="4d3f0-119">Vous pouvez faire référence toohello [référence d’applet de commande PowerShell Analytique de journal](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) pour d’autres fonctions.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="4d3f0-120">Analytique de journal s’appelait auparavant Operational Insights, c’est pourquoi il est le nom hello utilisé dans les applets de commande hello.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4d3f0-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4d3f0-121">Prerequisites</span></span>
<span data-ttu-id="4d3f0-122">Ces exemples de travail avec la version 2.3.0 ou ultérieure de module de AzureRm.OperationalInsights hello.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="4d3f0-123">Créer et configurer un espace de travail Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4d3f0-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="4d3f0-124">Hello exemple de script suivant illustre comment :</span><span class="sxs-lookup"><span data-stu-id="4d3f0-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="4d3f0-125">Créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="4d3f0-125">Create a workspace</span></span>
2. <span data-ttu-id="4d3f0-126">Liste des solutions disponibles hello</span><span class="sxs-lookup"><span data-stu-id="4d3f0-126">List hello available solutions</span></span>
3. <span data-ttu-id="4d3f0-127">Ajouter des solutions toohello espace de travail</span><span class="sxs-lookup"><span data-stu-id="4d3f0-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="4d3f0-128">Importer des recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="4d3f0-128">Import saved searches</span></span>
5. <span data-ttu-id="4d3f0-129">Exporter des recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="4d3f0-129">Export saved searches</span></span>
6. <span data-ttu-id="4d3f0-130">Créer un groupe d’ordinateurs</span><span class="sxs-lookup"><span data-stu-id="4d3f0-130">Create a computer group</span></span>
7. <span data-ttu-id="4d3f0-131">Activer la collecte de journaux IIS à partir d’ordinateurs avec l’agent Windows hello installé</span><span class="sxs-lookup"><span data-stu-id="4d3f0-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="4d3f0-132">Collecter les compteurs de performances de disque logique d’ordinateurs Linux (% d’Inodes utilisés, Mo libres, % d’espace utilisé, Transferts disque/s, Lectures disque/s, Écritures disque/s)</span><span class="sxs-lookup"><span data-stu-id="4d3f0-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="4d3f0-133">Collecter les événements Syslog d’ordinateurs Linux</span><span class="sxs-lookup"><span data-stu-id="4d3f0-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="4d3f0-134">Collecter les événements d’erreur et avertissement hello journal des événements à partir d’ordinateurs Windows</span><span class="sxs-lookup"><span data-stu-id="4d3f0-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="4d3f0-135">Collecter le compteur de performances Mo de mémoire disponible d’ordinateurs Windows</span><span class="sxs-lookup"><span data-stu-id="4d3f0-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="4d3f0-136">Collecter un journal personnalisé</span><span class="sxs-lookup"><span data-stu-id="4d3f0-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="4d3f0-137">Configuration Analytique de journal tooindex diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="4d3f0-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="4d3f0-138">Pour l’analyse sans agent des ressources Azure, les ressources de hello doivent toohave diagnostics Azure activé et configuré toowrite tooa Analytique de journal espace de travail.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="4d3f0-139">Cette approche envoie des données directement tooLog Analytique et ne nécessite pas de toobe de données écrit le compte de stockage tooa.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="4d3f0-140">Les ressources prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d3f0-140">Supported resources include:</span></span>

| <span data-ttu-id="4d3f0-141">Type de ressource</span><span class="sxs-lookup"><span data-stu-id="4d3f0-141">Resource Type</span></span> | <span data-ttu-id="4d3f0-142">Journaux</span><span class="sxs-lookup"><span data-stu-id="4d3f0-142">Logs</span></span> | <span data-ttu-id="4d3f0-143">Mesures</span><span class="sxs-lookup"><span data-stu-id="4d3f0-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d3f0-144">Passerelles d’application</span><span class="sxs-lookup"><span data-stu-id="4d3f0-144">Application Gateways</span></span>    | <span data-ttu-id="4d3f0-145">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-145">Yes</span></span> | <span data-ttu-id="4d3f0-146">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-146">Yes</span></span> |
| <span data-ttu-id="4d3f0-147">Comptes Automation</span><span class="sxs-lookup"><span data-stu-id="4d3f0-147">Automation accounts</span></span>     | <span data-ttu-id="4d3f0-148">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-148">Yes</span></span> | |
| <span data-ttu-id="4d3f0-149">Comptes Batch</span><span class="sxs-lookup"><span data-stu-id="4d3f0-149">Batch accounts</span></span>          | <span data-ttu-id="4d3f0-150">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-150">Yes</span></span> | <span data-ttu-id="4d3f0-151">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-151">Yes</span></span> |
| <span data-ttu-id="4d3f0-152">Data Lake analytics</span><span class="sxs-lookup"><span data-stu-id="4d3f0-152">Data Lake analytics</span></span>     | <span data-ttu-id="4d3f0-153">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-153">Yes</span></span> | | 
| <span data-ttu-id="4d3f0-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4d3f0-154">Data Lake store</span></span>         | <span data-ttu-id="4d3f0-155">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-155">Yes</span></span> | |
| <span data-ttu-id="4d3f0-156">Pool élastique SQL</span><span class="sxs-lookup"><span data-stu-id="4d3f0-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="4d3f0-157">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-157">Yes</span></span> |
| <span data-ttu-id="4d3f0-158">Espace de noms Event Hub</span><span class="sxs-lookup"><span data-stu-id="4d3f0-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="4d3f0-159">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-159">Yes</span></span> |
| <span data-ttu-id="4d3f0-160">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="4d3f0-160">IoT Hubs</span></span>                |     | <span data-ttu-id="4d3f0-161">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-161">Yes</span></span> |
| <span data-ttu-id="4d3f0-162">Key Vault</span><span class="sxs-lookup"><span data-stu-id="4d3f0-162">Key Vault</span></span>               | <span data-ttu-id="4d3f0-163">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-163">Yes</span></span> | |
| <span data-ttu-id="4d3f0-164">Équilibreurs de charge</span><span class="sxs-lookup"><span data-stu-id="4d3f0-164">Load Balancers</span></span>          | <span data-ttu-id="4d3f0-165">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-165">Yes</span></span> | |
| <span data-ttu-id="4d3f0-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4d3f0-166">Logic Apps</span></span>              | <span data-ttu-id="4d3f0-167">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-167">Yes</span></span> | <span data-ttu-id="4d3f0-168">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-168">Yes</span></span> |
| <span data-ttu-id="4d3f0-169">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="4d3f0-169">Network Security Groups</span></span> | <span data-ttu-id="4d3f0-170">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-170">Yes</span></span> | |
| <span data-ttu-id="4d3f0-171">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="4d3f0-171">Redis Cache</span></span>             |     | <span data-ttu-id="4d3f0-172">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-172">Yes</span></span> |
| <span data-ttu-id="4d3f0-173">Services de recherche</span><span class="sxs-lookup"><span data-stu-id="4d3f0-173">Search services</span></span>         | <span data-ttu-id="4d3f0-174">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-174">Yes</span></span> | <span data-ttu-id="4d3f0-175">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-175">Yes</span></span> |
| <span data-ttu-id="4d3f0-176">Espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="4d3f0-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="4d3f0-177">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-177">Yes</span></span> |
| <span data-ttu-id="4d3f0-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="4d3f0-178">SQL (v12)</span></span>               |     | <span data-ttu-id="4d3f0-179">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-179">Yes</span></span> |
| <span data-ttu-id="4d3f0-180">Sites web</span><span class="sxs-lookup"><span data-stu-id="4d3f0-180">Web Sites</span></span>               |     | <span data-ttu-id="4d3f0-181">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-181">Yes</span></span> |
| <span data-ttu-id="4d3f0-182">Batteries de serveurs web</span><span class="sxs-lookup"><span data-stu-id="4d3f0-182">Web Server farms</span></span>        |     | <span data-ttu-id="4d3f0-183">Oui</span><span class="sxs-lookup"><span data-stu-id="4d3f0-183">Yes</span></span> |

<span data-ttu-id="4d3f0-184">Pour plus d’informations hello de métriques disponibles de hello, consultez trop[prise en charge des métriques avec Azure analyse](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4d3f0-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="4d3f0-185">Pour plus d’informations hello de journaux disponibles de hello, consultez trop[prise en charge des services et schéma pour les journaux de diagnostic](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4d3f0-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="4d3f0-186">Vous pouvez également utiliser hello précédant les journaux de toocollect d’applet de commande à partir des ressources qui se trouvent dans différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="4d3f0-187">Hello est en mesure de toowork entre abonnements étant donné que vous fournissez un id de hello de ces deux ressources hello créer des journaux et des journaux de hello hello espace de travail sont envoyées à.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="4d3f0-188">Configuration tooindex Analytique de journal des diagnostics Windows Azure à partir du stockage</span><span class="sxs-lookup"><span data-stu-id="4d3f0-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="4d3f0-189">toocollect journal des données à partir d’une instance en cours d’exécution d’un service cloud classique ou d’un cluster service fabric, vous avez besoin de stockage tooAzure toofirst écriture hello.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="4d3f0-190">Analytique de journal est alors configuré de journaux de hello toocollect hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="4d3f0-191">Les ressources prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d3f0-191">Supported resources include:</span></span>

* <span data-ttu-id="4d3f0-192">Services cloud classiques (rôles de travail et web)</span><span class="sxs-lookup"><span data-stu-id="4d3f0-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="4d3f0-193">Clusters Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d3f0-193">Service fabric clusters</span></span>

<span data-ttu-id="4d3f0-194">Hello suivant montre l’exemple de comment pour :</span><span class="sxs-lookup"><span data-stu-id="4d3f0-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="4d3f0-195">Liste des comptes de stockage existant hello et emplacements Analytique de journal indexe les données à partir de</span><span class="sxs-lookup"><span data-stu-id="4d3f0-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="4d3f0-196">Créer un tooread de configuration à partir d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="4d3f0-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="4d3f0-197">Mettre à jour hello nouvellement créé tooindex les données de configuration à partir des emplacements supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4d3f0-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="4d3f0-198">Suppression de la configuration de hello qui vient d’être créé</span><span class="sxs-lookup"><span data-stu-id="4d3f0-198">Delete hello newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="4d3f0-199">Vous pouvez également utiliser hello précédant les journaux de toocollect de script à partir de comptes de stockage dans des abonnements différents.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="4d3f0-200">le script de Hello est en mesure de toowork entre abonnements étant donné que vous fournissez des id de ressource de compte de stockage hello et une clé d’accès correspondante.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="4d3f0-201">Lorsque vous modifiez la clé d’accès hello, vous devez tooupdate hello insight toohave hello nouvelle clé de stockage.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4d3f0-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d3f0-202">Next steps</span></span>
* <span data-ttu-id="4d3f0-203">[Passez en revue les applets de commande PowerShell de Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) pour obtenir plus d’informations sur l’utilisation de PowerShell pour configurer Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4d3f0-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

