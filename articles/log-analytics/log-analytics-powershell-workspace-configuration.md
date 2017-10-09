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
# <a name="manage-log-analytics-using-powershell"></a>Gérer Log Analytics à l’aide de PowerShell
Vous pouvez utiliser hello [applets de commande PowerShell Analytique de journal](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform diverses fonctions dans Analytique de journal à partir d’une ligne de commande ou dans le cadre d’un script.  Voici quelques exemples de tâches hello que vous pouvez effectuer avec PowerShell :

* Créer un espace de travail
* Ajouter ou supprimer une solution
* Importer et exporter des recherches enregistrées
* Créer un groupe d’ordinateurs
* Activer la collecte de journaux IIS à partir d’ordinateurs avec l’agent Windows hello installé
* Collecter les compteurs de performances d’ordinateurs Linux et Windows
* Collecter les événements de Syslog sur des ordinateurs Linux 
* Collecter les événements des journaux des événements Windows
* Collecter des journaux des événements personnalisés
* Ajouter hello journal analytique agent tooan machine virtuelle Azure
* Configurer le journal analytique tooindex collectées à l’aide des diagnostics Windows Azure

Cet article fournit deux exemples de code qui illustrent les fonctions hello que vous pouvez effectuer à partir de PowerShell.  Vous pouvez faire référence toohello [référence d’applet de commande PowerShell Analytique de journal](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) pour d’autres fonctions.

> [!NOTE]
> Analytique de journal s’appelait auparavant Operational Insights, c’est pourquoi il est le nom hello utilisé dans les applets de commande hello.
> 
> 

## <a name="prerequisites"></a>Composants requis
Ces exemples de travail avec la version 2.3.0 ou ultérieure de module de AzureRm.OperationalInsights hello.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Créer et configurer un espace de travail Log Analytics
Hello exemple de script suivant illustre comment :

1. Créer un espace de travail
2. Liste des solutions disponibles hello
3. Ajouter des solutions toohello espace de travail
4. Importer des recherches enregistrées
5. Exporter des recherches enregistrées
6. Créer un groupe d’ordinateurs
7. Activer la collecte de journaux IIS à partir d’ordinateurs avec l’agent Windows hello installé
8. Collecter les compteurs de performances de disque logique d’ordinateurs Linux (% d’Inodes utilisés, Mo libres, % d’espace utilisé, Transferts disque/s, Lectures disque/s, Écritures disque/s)
9. Collecter les événements Syslog d’ordinateurs Linux
10. Collecter les événements d’erreur et avertissement hello journal des événements à partir d’ordinateurs Windows
11. Collecter le compteur de performances Mo de mémoire disponible d’ordinateurs Windows
12. Collecter un journal personnalisé 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Configuration Analytique de journal tooindex diagnostics Azure
Pour l’analyse sans agent des ressources Azure, les ressources de hello doivent toohave diagnostics Azure activé et configuré toowrite tooa Analytique de journal espace de travail. Cette approche envoie des données directement tooLog Analytique et ne nécessite pas de toobe de données écrit le compte de stockage tooa. Les ressources prises en charge sont les suivantes :

| Type de ressource | Journaux | Mesures |
| --- | --- | --- |
| Passerelles d’application    | Oui | Oui |
| Comptes Automation     | Oui | |
| Comptes Batch          | Oui | Oui |
| Data Lake analytics     | Oui | | 
| Data Lake Store         | Oui | |
| Pool élastique SQL        |     | Oui |
| Espace de noms Event Hub     |     | Oui |
| IoT Hubs                |     | Oui |
| Key Vault               | Oui | |
| Équilibreurs de charge          | Oui | |
| Logic Apps              | Oui | Oui |
| Groupes de sécurité réseau | Oui | |
| Cache Redis             |     | Oui |
| Services de recherche         | Oui | Oui |
| Espace de noms Service Bus   |     | Oui |
| SQL (v12)               |     | Oui |
| Sites web               |     | Oui |
| Batteries de serveurs web        |     | Oui |

Pour plus d’informations hello de métriques disponibles de hello, consultez trop[prise en charge des métriques avec Azure analyse](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Pour plus d’informations hello de journaux disponibles de hello, consultez trop[prise en charge des services et schéma pour les journaux de diagnostic](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

Vous pouvez également utiliser hello précédant les journaux de toocollect d’applet de commande à partir des ressources qui se trouvent dans différents abonnements. Hello est en mesure de toowork entre abonnements étant donné que vous fournissez un id de hello de ces deux ressources hello créer des journaux et des journaux de hello hello espace de travail sont envoyées à.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Configuration tooindex Analytique de journal des diagnostics Windows Azure à partir du stockage
toocollect journal des données à partir d’une instance en cours d’exécution d’un service cloud classique ou d’un cluster service fabric, vous avez besoin de stockage tooAzure toofirst écriture hello. Analytique de journal est alors configuré de journaux de hello toocollect hello compte de stockage. Les ressources prises en charge sont les suivantes :

* Services cloud classiques (rôles de travail et web)
* Clusters Service Fabric

Hello suivant montre l’exemple de comment pour :

1. Liste des comptes de stockage existant hello et emplacements Analytique de journal indexe les données à partir de
2. Créer un tooread de configuration à partir d’un compte de stockage
3. Mettre à jour hello nouvellement créé tooindex les données de configuration à partir des emplacements supplémentaires
4. Suppression de la configuration de hello qui vient d’être créé

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

Vous pouvez également utiliser hello précédant les journaux de toocollect de script à partir de comptes de stockage dans des abonnements différents. le script de Hello est en mesure de toowork entre abonnements étant donné que vous fournissez des id de ressource de compte de stockage hello et une clé d’accès correspondante. Lorsque vous modifiez la clé d’accès hello, vous devez tooupdate hello insight toohave hello nouvelle clé de stockage.


## <a name="next-steps"></a>Étapes suivantes
* [Passez en revue les applets de commande PowerShell de Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) pour obtenir plus d’informations sur l’utilisation de PowerShell pour configurer Log Analytics.

