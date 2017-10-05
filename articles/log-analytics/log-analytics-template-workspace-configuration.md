---
title: "Utilisation de modèles Azure Resource Manager pour créer et configurer un espace de travail Log Analytics | Microsoft Docs"
description: "Vous pouvez utiliser des modèles Azure Resource Manager pour créer et configurer des espaces de travail Log Analytics."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: d21ca1b0-847d-4716-bb30-2a8c02a606aa
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: json
ms.topic: article
ms.date: 06/01/2017
ms.author: richrund
ms.openlocfilehash: 505b741d14c594b22108298466c646bf723ce2d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-log-analytics-using-azure-resource-manager-templates"></a><span data-ttu-id="7faf6-103">Gérer Log Analytics à l’aide de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7faf6-103">Manage Log Analytics using Azure Resource Manager templates</span></span>
<span data-ttu-id="7faf6-104">Vous pouvez utiliser des [modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) pour créer et configurer des espaces de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7faf6-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to create and configure Log Analytics workspaces.</span></span> <span data-ttu-id="7faf6-105">Voici quelques exemples de tâches que vous pouvez effectuer avec des modèles :</span><span class="sxs-lookup"><span data-stu-id="7faf6-105">Examples of the tasks you can perform with templates include:</span></span>

* <span data-ttu-id="7faf6-106">Créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="7faf6-106">Create a workspace</span></span>
* <span data-ttu-id="7faf6-107">Ajouter une solution</span><span class="sxs-lookup"><span data-stu-id="7faf6-107">Add a solution</span></span>
* <span data-ttu-id="7faf6-108">Créer des recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="7faf6-108">Create saved searches</span></span>
* <span data-ttu-id="7faf6-109">Créer un groupe d’ordinateurs</span><span class="sxs-lookup"><span data-stu-id="7faf6-109">Create a computer group</span></span>
* <span data-ttu-id="7faf6-110">Activer la collecte de journaux IIS à partir d’ordinateurs sur lesquels l’agent Windows est installé</span><span class="sxs-lookup"><span data-stu-id="7faf6-110">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="7faf6-111">Collecter les compteurs de performances d’ordinateurs Linux et Windows</span><span class="sxs-lookup"><span data-stu-id="7faf6-111">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="7faf6-112">Collecter les événements de Syslog sur des ordinateurs Linux</span><span class="sxs-lookup"><span data-stu-id="7faf6-112">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="7faf6-113">Collecter les événements des journaux des événements Windows</span><span class="sxs-lookup"><span data-stu-id="7faf6-113">Collect events from Windows event logs</span></span>
* <span data-ttu-id="7faf6-114">Collecter des journaux des événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="7faf6-114">Collect custom event logs</span></span>
* <span data-ttu-id="7faf6-115">Ajouter l’agent Log Analytics à une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="7faf6-115">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="7faf6-116">Configurer Log Analytics pour indexer les données collectées à l’aide des diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="7faf6-116">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="7faf6-117">Cet article fournit des exemples de modèle qui illustrent des opérations de configuration que vous pouvez effectuer à partir de modèles.</span><span class="sxs-lookup"><span data-stu-id="7faf6-117">This article provides a template samples that illustrate some of the configuration that you can perform from templates.</span></span>

## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="7faf6-118">Créer et configurer un espace de travail Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7faf6-118">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="7faf6-119">L’exemple de modèle suivant illustre comment :</span><span class="sxs-lookup"><span data-stu-id="7faf6-119">The following template sample illustrates how to:</span></span>

1. <span data-ttu-id="7faf6-120">Créer un espace de travail, y compris la rétention des données de paramètres</span><span class="sxs-lookup"><span data-stu-id="7faf6-120">Create a workspace, including setting data retention</span></span>
2. <span data-ttu-id="7faf6-121">Ajouter des solutions à l’espace de travail</span><span class="sxs-lookup"><span data-stu-id="7faf6-121">Add solutions to the workspace</span></span>
3. <span data-ttu-id="7faf6-122">Créer des recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="7faf6-122">Create saved searches</span></span>
4. <span data-ttu-id="7faf6-123">Créer un groupe d’ordinateurs</span><span class="sxs-lookup"><span data-stu-id="7faf6-123">Create a computer group</span></span>
5. <span data-ttu-id="7faf6-124">Activer la collecte de journaux IIS à partir d’ordinateurs sur lesquels l’agent Windows est installé</span><span class="sxs-lookup"><span data-stu-id="7faf6-124">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
6. <span data-ttu-id="7faf6-125">Collecter les compteurs de performances de disque logique d’ordinateurs Linux (% d’Inodes utilisés, Mo libres, % d’espace utilisé, Transferts disque/s, Lectures disque/s, Écritures disque/s)</span><span class="sxs-lookup"><span data-stu-id="7faf6-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
7. <span data-ttu-id="7faf6-126">Collecter les événements Syslog d’ordinateurs Linux</span><span class="sxs-lookup"><span data-stu-id="7faf6-126">Collect syslog events from Linux computers</span></span>
8. <span data-ttu-id="7faf6-127">Collecter les événements d’erreur et d’avertissement du journal des événements d’application d’ordinateurs Windows</span><span class="sxs-lookup"><span data-stu-id="7faf6-127">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
9. <span data-ttu-id="7faf6-128">Collecter le compteur de performances Mo de mémoire disponible d’ordinateurs Windows</span><span class="sxs-lookup"><span data-stu-id="7faf6-128">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
10. <span data-ttu-id="7faf6-129">Collecter un journal personnalisé</span><span class="sxs-lookup"><span data-stu-id="7faf6-129">Collect a custom log</span></span> 
11. <span data-ttu-id="7faf6-130">Collecter les journaux IIS et les journaux des événements Windows écrits par les diagnostics Azure dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="7faf6-130">Collect IIS logs and Windows Event logs written by Azure diagnostics to a storage account</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "description": "workspaceName"
      }
    },
    "serviceTier": {
      "type": "string",
      "allowedValues": [
        "Free",
        "Standalone",
        "PerNode"
      ],
      "metadata": {
        "description": "Service Tier: Free, Standalone, or PerNode"
    }
      },
    "dataRetention": {
      "type": "int",
      "defaultValue": 30,
      "minValue": 7,
      "maxValue": 730,
      "metadata": {
        "description": "Number of days of retention. Free plans can only have 7 days, Standalone and OMS plans include 30 days for free"
      }
    },
    "location": {
      "type": "string",
      "allowedValues": [
        "East US",
        "West Europe",
        "Southeast Asia",
        "Australia Southeast"
      ]
    },
    "applicationDiagnosticsStorageAccountName": {
        "type": "string",
        "metadata": {
          "description": "Name of the storage account with Azure diagnostics output"
        }
    },
    "applicationDiagnosticsStorageAccountResourceGroup": {
        "type": "string",
        "metadata": {
          "description": "The resource group name containing the storage account with Azure diagnostics output"
        }
    }
  },
  "variables": {
    "Updates": {
      "Name": "[Concat('Updates', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "Updates"
    },
    "AntiMalware": {
      "Name": "[concat('AntiMalware', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "AntiMalware"
    },
    "SQLAssessment": {
      "Name": "[Concat('SQLAssessment', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "SQLAssessment"
    },
    "diagnosticsStorageAccount": "[resourceId(parameters('applicationDiagnosticsStorageAccountResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName'))]"
  },
  "resources": [
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationalInsights/workspaces",
      "name": "[parameters('workspaceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "sku": {
          "Name": "[parameters('serviceTier')]"
        },
    "retention": "[parameters('dataRetention')]"
      },
      "resources": [
        {
          "apiVersion": "2015-11-01-preview",
          "name": "VMSS Queries2",
          "type": "savedSearches",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "Category": "VMSS",
            "ETag": "*",
            "DisplayName": "VMSS Instance Count",
            "Query": "Type:Event Source=ServiceFabricNodeBootstrapAgent | dedup Computer | measure count () by Computer",
            "Version": 1
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsEvent1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsEvent",
          "properties": {
            "eventLogName": "Application",
            "eventTypes": [
              {
                "eventType": "Error"
              },
              {
                "eventType": "Warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsPerfCounter1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsPerformanceCounter",
          "properties": {
            "objectName": "Memory",
            "instanceName": "*",
            "intervalSeconds": 10,
            "counterName": "Available MBytes"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleIISLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "IISLogs",
          "properties": {
            "state": "OnPremiseEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslog",
          "properties": {
            "syslogName": "kern",
            "syslogSeverities": [
              {
                "severity": "emerg"
              },
              {
                "severity": "alert"
              },
              {
                "severity": "crit"
              },
              {
                "severity": "err"
              },
              {
                "severity": "warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslogCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerf1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceObject",
          "properties": {
            "performanceCounters": [
              {
                "counterName": "% Used Inodes"
              },
              {
                "counterName": "Free Megabytes"
              },
              {
                "counterName": "% Used Space"
              },
              {
                "counterName": "Disk Transfers/sec"
              },
              {
                "counterName": "Disk Reads/sec"
              },
              {
                "counterName": "Disk Writes/sec"
              }
            ],
            "objectName": "Logical Disk",
            "instanceName": "*",
            "intervalSeconds": 10
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerfCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLog",
          "properties": {
            "customLogName": "sampleCustomLog1",
            "description": "test custom log datasources",
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
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLogCollection",
          "properties": {
            "state": "LinuxLogsEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "name": "[concat(parameters('applicationDiagnosticsStorageAccountName'),parameters('workspaceName'))]",
          "type": "storageinsightconfigs",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "containers": [ 
              "wad-iis-logfiles" 
            ],
            "tables": [
              "WADWindowsEventLogsTable"
            ],
            "storageAccount": {
              "id": "[variables('diagnosticsStorageAccount')]",
              "key": "[listKeys(variables('diagnosticsStorageAccount'),'2015-06-15').key1]"
            }
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('Updates').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('Updates').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('Updates').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('Updates').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('AntiMalware').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('AntiMalware').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('AntiMalware').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('AntiMalware').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('SQLAssessment').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('SQLAssessment').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('SQLAssessment').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('SQLAssessment').GalleryName)]",
            "promotionCode": ""
          }
        }
      ]
    }
  ],
  "outputs": {
    "workspaceOutput": {
      "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-11-01-preview')]",
      "type": "object"
    }
  }
}

```
### <a name="deploying-the-sample-template"></a><span data-ttu-id="7faf6-131">Déploiement de l’exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="7faf6-131">Deploying the sample template</span></span>
<span data-ttu-id="7faf6-132">Pour déployer l’exemple de modèle :</span><span class="sxs-lookup"><span data-stu-id="7faf6-132">To deploy the sample template:</span></span>

1. <span data-ttu-id="7faf6-133">Enregistrez l’exemple joint dans un fichier, par exemple `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="7faf6-133">Save the attached sample in a file, for example `azuredeploy.json`</span></span> 
2. <span data-ttu-id="7faf6-134">Modifiez le modèle afin de disposer de la configuration souhaitée.</span><span class="sxs-lookup"><span data-stu-id="7faf6-134">Edit the template to have the configuration you want</span></span>
3. <span data-ttu-id="7faf6-135">Utilisez PowerShell ou la ligne de commande pour déployer le modèle.</span><span class="sxs-lookup"><span data-stu-id="7faf6-135">Use PowerShell or the command line to deploy the template</span></span>

#### <a name="powershell"></a><span data-ttu-id="7faf6-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7faf6-136">PowerShell</span></span>
`New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile azuredeploy.json`

#### <a name="command-line"></a><span data-ttu-id="7faf6-137">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="7faf6-137">Command line</span></span>
```
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile azuredeploy.json
```


## <a name="example-resource-manager-templates"></a><span data-ttu-id="7faf6-138">Exemples de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7faf6-138">Example Resource Manager templates</span></span>
<span data-ttu-id="7faf6-139">La galerie de modèles de démarrage rapide Azure comprend plusieurs modèles pour Log Analytics, destinés aux opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7faf6-139">The Azure quickstart template gallery includes several templates for Log Analytics, including:</span></span>

* [<span data-ttu-id="7faf6-140">Déployer une machine virtuelle exécutant Windows avec l’extension de machine virtuelle Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7faf6-140">Deploy a virtual machine running Windows with the Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-windows-vm/)
* [<span data-ttu-id="7faf6-141">Déployer une machine virtuelle exécutant Linux avec l’extension de machine virtuelle Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7faf6-141">Deploy a virtual machine running Linux with the Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-ubuntu-vm/)
* [<span data-ttu-id="7faf6-142">Analyser Azure Site Recovery à l’aide d’un espace de travail Log Analytics existant</span><span class="sxs-lookup"><span data-stu-id="7faf6-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/asr-oms-monitoring/)
* [<span data-ttu-id="7faf6-143">Analyser les applications web Azure à l’aide d’un espace de travail Log Analytics existant</span><span class="sxs-lookup"><span data-stu-id="7faf6-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-webappazure-oms-monitoring/)
* [<span data-ttu-id="7faf6-144">Analyser SQL Azure à l’aide d’un espace de travail Log Analytics existant</span><span class="sxs-lookup"><span data-stu-id="7faf6-144">Monitor SQL Azure using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-sqlazure-oms-monitoring/)
* [<span data-ttu-id="7faf6-145">Déployer un cluster Service Fabric et l’analyser avec un espace de travail Log Analytics existant</span><span class="sxs-lookup"><span data-stu-id="7faf6-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-oms/)
* [<span data-ttu-id="7faf6-146">Déployer un cluster Service Fabric et créer un espace de travail Log Analytics pour le surveiller</span><span class="sxs-lookup"><span data-stu-id="7faf6-146">Deploy a Service Fabric cluster and create a Log Analytics workspace to monitor it</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-vmss-oms/)

## <a name="next-steps"></a><span data-ttu-id="7faf6-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7faf6-147">Next steps</span></span>
* [<span data-ttu-id="7faf6-148">Déployer des agents dans des machines virtuelles Azure en utilisant des modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7faf6-148">Deploy agents into Azure VMs using Resource Manager templates</span></span>](log-analytics-azure-vm-extension.md)

