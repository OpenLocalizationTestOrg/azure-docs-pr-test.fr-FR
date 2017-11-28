---
title: "Activer automatiquement les paramètres de diagnostic à l’aide d’un modèle Resource Manager | Microsoft Docs"
description: "Découvrez comment utiliser un modèle Resource Manager pour créer des paramètres de diagnostic qui activeront la diffusion en continu de vos journaux de diagnostic vers Event Hubs ou leur stockage dans un compte de stockage."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="be705-103">Activer automatiquement les paramètres de diagnostic lors de la création de ressources à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be705-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="be705-104">Dans cet article, nous vous expliquons comment utiliser un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) pour configurer les paramètres de diagnostic d’une ressource lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="be705-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="be705-105">Cela vous permet de démarrer automatiquement la diffusion en continu de vos journaux de diagnostic et des mesures vers Event Hubs, leur archivage dans un compte de stockage ou leur envoi à Log Analytics lorsqu’une ressource est créée.</span><span class="sxs-lookup"><span data-stu-id="be705-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="be705-106">La méthode d’activation des journaux de diagnostic à l’aide d’un modèle Resource Manager varie selon le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="be705-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="be705-107">Les ressources **Non-Compute** (comme Network Security Groups, Logic Apps, Automation) utilisent les [paramètres de diagnostic décrits dans cet article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="be705-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="be705-108">**de calcul** (basées sur WAD/LAD) utilisent le [fichier de configuration de WAD/LAD décrit dans cet article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="be705-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="be705-109">Dans cet article, nous expliquons comment configurer les diagnostics à l’aide de deux méthodes.</span><span class="sxs-lookup"><span data-stu-id="be705-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="be705-110">Procédure de base :</span><span class="sxs-lookup"><span data-stu-id="be705-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="be705-111">Créez un modèle sous la forme d’un fichier JSON qui décrit comment créer la ressource et activer les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="be705-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="be705-112">[Déployez le modèle à l’aide de n’importe quelle méthode de déploiement](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="be705-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="be705-113">Ci-dessous, nous vous donnons un exemple de modèle de fichier JSON que vous devez générer pour les ressources de calcul et non liées au calcul.</span><span class="sxs-lookup"><span data-stu-id="be705-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="be705-114">Modèle de ressource non liée au calcul</span><span class="sxs-lookup"><span data-stu-id="be705-114">Non-Compute resource template</span></span>
<span data-ttu-id="be705-115">Pour les ressources non liées au calcul, vous devrez effectuer les deux opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="be705-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="be705-116">Ajouter des paramètres à l’objet Blob de paramètres pour le nom de compte de stockage, l’ID de règle de Service Bus et/ou l’ID d’espace de travail OMS Log Analytics (activation de l’archivage des journaux de diagnostic dans un compte de stockage, de la diffusion en continu des journaux vers Event Hubs et/ou de l’envoi de journaux à Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="be705-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="be705-117">Ajouter une ressource de type `[resource namespace]/providers/diagnosticSettings`dans le tableau de ressources de la ressource pour laquelle vous souhaitez activer les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="be705-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="be705-118">L’objet blob de propriétés pour le paramètre de diagnostic suit [le format décrit dans cet article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="be705-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="be705-119">Ajouter la propriété `metrics` vous permettra d’envoyer également des mesures sur la ressource à ces mêmes sorties, à condition que [la ressource prenne en charge les mesures Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="be705-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="be705-120">Voici un exemple complet qui crée une application logique et active la diffusion en continu vers Event Hubs et le stockage dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="be705-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="be705-121">Modèle de ressource de calcul</span><span class="sxs-lookup"><span data-stu-id="be705-121">Compute resource template</span></span>
<span data-ttu-id="be705-122">Pour activer les diagnostics pour une ressource de calcul, par exemple un cluster Service Fabric ou une machine virtuelle, vous devez :</span><span class="sxs-lookup"><span data-stu-id="be705-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="be705-123">Ajouter l’extension Azure Diagnostics à la définition de ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="be705-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="be705-124">Spécifier un compte de stockage et/ou un Event Hub comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="be705-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="be705-125">Ajouter le contenu de votre fichier WADCfg XML dans la propriété XMLCfg, en échappant correctement tous les caractères XML.</span><span class="sxs-lookup"><span data-stu-id="be705-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="be705-126">Cette dernière étape peut être difficile à réaliser.</span><span class="sxs-lookup"><span data-stu-id="be705-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="be705-127">[Consultez cet article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) pour obtenir un exemple qui montre comment fractionner le schéma de configuration de diagnostics en variables échappées et mises en forme correctement.</span><span class="sxs-lookup"><span data-stu-id="be705-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="be705-128">L’intégralité du processus, y compris des exemples, est décrite [dans ce document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be705-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="be705-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be705-129">Next Steps</span></span>
* [<span data-ttu-id="be705-130">En savoir plus sur les journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="be705-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="be705-131">Stream Azure Diagnostic Logs to Event Hubs (Diffuser en continu les journaux de diagnostic Azure vers Event Hubs)</span><span class="sxs-lookup"><span data-stu-id="be705-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

