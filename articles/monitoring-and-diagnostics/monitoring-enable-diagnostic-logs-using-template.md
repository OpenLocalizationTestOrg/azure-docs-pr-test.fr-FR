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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Activer automatiquement les paramètres de diagnostic lors de la création de ressources à l’aide d’un modèle Resource Manager
Dans cet article, nous montrons comment vous pouvez utiliser un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure les paramètres de Diagnostic sur une ressource lors de sa création. Cela vous permet de démarrer tooautomatically votre tooEvent journaux de Diagnostic et les mesures de concentrateurs, en les archivant dans un compte de stockage, ou en les envoyant tooLog Analytique lors de la création d’une ressource de diffusion en continu.

méthode Hello pour activer les journaux de Diagnostic à l’aide d’un modèle de gestionnaire de ressources dépend du type de ressource hello.

* Les ressources **Non-Compute** (comme Network Security Groups, Logic Apps, Automation) utilisent les [paramètres de diagnostic décrits dans cet article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Calcul** (WAD/SCÉNARISTE basé) les ressources utilisent hello [fichier de configuration de Diagnostics Windows AZURE/SCÉNARISTE décrit dans cet article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

Dans cet article, nous décrivons comment tooconfigure les diagnostics à l’aide de ces deux méthodes.

les étapes de base Hello sont les suivantes :

1. Créer un modèle en tant qu’un fichier JSON qui décrit comment toocreate hello ressource et activer les diagnostics.
2. [Déployer à l’aide de n’importe quelle méthode de déploiement de modèle de hello](../azure-resource-manager/resource-group-template-deploy.md).

Ci-dessous, nous donner un exemple de modèle de hello fichier JSON, vous devez toogenerate pour non calculés et les ressources de calcul.

## <a name="non-compute-resource-template"></a>Modèle de ressource non liée au calcul
Pour les ressources non calculés, vous devez toodo deux choses :

1. Ajouter des paramètres toohello paramètres objet blob pour nom de compte de stockage hello, ID de règle de bus de service et/ou ID d’espace de travail Analytique des journaux OMS (permettant d’archivage de journaux de Diagnostic dans un compte de stockage, la diffusion en continu de journaux tooEvent concentrateurs et/ou l’envoi de journaux tooLog Analytique).
   
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
2. Dans le tableau de ressources hello de ressource hello pour lequel vous souhaitez tooenable les journaux de Diagnostic, ajoutez une ressource de type `[resource namespace]/providers/diagnosticSettings`.
   
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

suit Hello blob de propriétés pour le paramètre de Diagnostic de hello [format hello décrit dans cet article](https://msdn.microsoft.com/library/azure/dn931931.aspx). Ajout de hello `metrics` propriété activera toothese de métriques tooalso envoi ressources même génère, à condition que [les ressources hello prend en charge les métriques de moniteur de Windows Azure](monitoring-supported-metrics.md).

Voici un exemple complet qui crée une application de la logique et Active la diffusion en continu tooEvent concentrateurs et stockage dans un compte de stockage.

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

## <a name="compute-resource-template"></a>Modèle de ressource de calcul
tooenable des diagnostics sur une ressource de calcul, par exemple un ordinateur virtuel ou un cluster Service Fabric, vous devez :

1. Ajouter la définition de ressource d’ordinateur virtuel toohello hello Azure Diagnostics extension.
2. Spécifier un compte de stockage et/ou un Event Hub comme paramètre.
3. Ajouter le contenu hello de votre fichier WADCfg XML dans la propriété XMLCfg de hello, séquence d’échappement tous les caractères XML correctement.

> [!WARNING]
> Cette dernière étape peut être délicate tooget droite. [Consultez l’article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) pour obtenir un exemple que fractionnements hello schéma de Configuration de Diagnostics dans des variables de séquence d’échappement et mise en forme correctement.
> 
> 

Hello tout processus, y compris les exemples, est décrite [dans ce document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les journaux de diagnostic Azure](monitoring-overview-of-diagnostic-logs.md)
* [Flux de données des journaux de Diagnostic Azure tooEvent concentrateurs](monitoring-stream-diagnostic-logs-to-event-hubs.md)

