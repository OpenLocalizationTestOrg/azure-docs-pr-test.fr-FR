---
title: "aaaAutomatically activer les paramètres de Diagnostic à l’aide d’un modèle de gestionnaire de ressources | Documents Microsoft"
description: "Découvrez comment toouse un gestionnaire de ressources modèle toocreate les paramètres de diagnostic qui vous permettront de toostream votre diagnostic tooEvent concentrateurs de journaux ou de les stocker dans un compte de stockage."
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
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="8ae26-103">Activer automatiquement les paramètres de diagnostic lors de la création de ressources à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ae26-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="8ae26-104">Dans cet article, nous montrons comment vous pouvez utiliser un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure les paramètres de Diagnostic sur une ressource lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="8ae26-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="8ae26-105">Cela vous permet de démarrer tooautomatically votre tooEvent journaux de Diagnostic et les mesures de concentrateurs, en les archivant dans un compte de stockage, ou en les envoyant tooLog Analytique lors de la création d’une ressource de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="8ae26-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="8ae26-106">méthode Hello pour activer les journaux de Diagnostic à l’aide d’un modèle de gestionnaire de ressources dépend du type de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="8ae26-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="8ae26-107">Les ressources **Non-Compute** (comme Network Security Groups, Logic Apps, Automation) utilisent les [paramètres de diagnostic décrits dans cet article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="8ae26-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="8ae26-108">**Calcul** (WAD/SCÉNARISTE basé) les ressources utilisent hello [fichier de configuration de Diagnostics Windows AZURE/SCÉNARISTE décrit dans cet article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="8ae26-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="8ae26-109">Dans cet article, nous décrivons comment tooconfigure les diagnostics à l’aide de ces deux méthodes.</span><span class="sxs-lookup"><span data-stu-id="8ae26-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="8ae26-110">les étapes de base Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ae26-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="8ae26-111">Créer un modèle en tant qu’un fichier JSON qui décrit comment toocreate hello ressource et activer les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="8ae26-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="8ae26-112">[Déployer à l’aide de n’importe quelle méthode de déploiement de modèle de hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8ae26-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="8ae26-113">Ci-dessous, nous donner un exemple de modèle de hello fichier JSON, vous devez toogenerate pour non calculés et les ressources de calcul.</span><span class="sxs-lookup"><span data-stu-id="8ae26-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="8ae26-114">Modèle de ressource non liée au calcul</span><span class="sxs-lookup"><span data-stu-id="8ae26-114">Non-Compute resource template</span></span>
<span data-ttu-id="8ae26-115">Pour les ressources non calculés, vous devez toodo deux choses :</span><span class="sxs-lookup"><span data-stu-id="8ae26-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="8ae26-116">Ajouter des paramètres toohello paramètres objet blob pour nom de compte de stockage hello, ID de règle de bus de service et/ou ID d’espace de travail Analytique des journaux OMS (permettant d’archivage de journaux de Diagnostic dans un compte de stockage, la diffusion en continu de journaux tooEvent concentrateurs et/ou l’envoi de journaux tooLog Analytique).</span><span class="sxs-lookup"><span data-stu-id="8ae26-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="8ae26-117">Dans le tableau de ressources hello de ressource hello pour lequel vous souhaitez tooenable les journaux de Diagnostic, ajoutez une ressource de type `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="8ae26-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="8ae26-118">suit Hello blob de propriétés pour le paramètre de Diagnostic de hello [format hello décrit dans cet article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ae26-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="8ae26-119">Ajout de hello `metrics` propriété activera toothese de métriques tooalso envoi ressources même génère, à condition que [les ressources hello prend en charge les métriques de moniteur de Windows Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="8ae26-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="8ae26-120">Voici un exemple complet qui crée une application de la logique et Active la diffusion en continu tooEvent concentrateurs et stockage dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8ae26-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="8ae26-121">Modèle de ressource de calcul</span><span class="sxs-lookup"><span data-stu-id="8ae26-121">Compute resource template</span></span>
<span data-ttu-id="8ae26-122">tooenable des diagnostics sur une ressource de calcul, par exemple un ordinateur virtuel ou un cluster Service Fabric, vous devez :</span><span class="sxs-lookup"><span data-stu-id="8ae26-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="8ae26-123">Ajouter la définition de ressource d’ordinateur virtuel toohello hello Azure Diagnostics extension.</span><span class="sxs-lookup"><span data-stu-id="8ae26-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="8ae26-124">Spécifier un compte de stockage et/ou un Event Hub comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="8ae26-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="8ae26-125">Ajouter le contenu hello de votre fichier WADCfg XML dans la propriété XMLCfg de hello, séquence d’échappement tous les caractères XML correctement.</span><span class="sxs-lookup"><span data-stu-id="8ae26-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="8ae26-126">Cette dernière étape peut être délicate tooget droite.</span><span class="sxs-lookup"><span data-stu-id="8ae26-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="8ae26-127">[Consultez l’article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) pour obtenir un exemple que fractionnements hello schéma de Configuration de Diagnostics dans des variables de séquence d’échappement et mise en forme correctement.</span><span class="sxs-lookup"><span data-stu-id="8ae26-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="8ae26-128">Hello tout processus, y compris les exemples, est décrite [dans ce document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ae26-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ae26-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ae26-129">Next Steps</span></span>
* [<span data-ttu-id="8ae26-130">En savoir plus sur les journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="8ae26-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="8ae26-131">Flux de données des journaux de Diagnostic Azure tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="8ae26-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

