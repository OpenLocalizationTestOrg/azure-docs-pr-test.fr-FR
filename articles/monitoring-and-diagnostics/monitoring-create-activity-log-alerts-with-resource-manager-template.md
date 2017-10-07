---
title: "une alerte de journal d’activité avec un modèle de gestionnaire de ressources d’aaaCreate | Documents Microsoft"
description: "Soyez informé lorsque vos ressources Azure sont créées."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Créer une alerte de journal d’activité avec un modèle Resource Manager
Cet article vous explique comment toouse un [modèle Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) alertes de journal d’activité tooconfigure. À l’aide de modèles, vous pouvez facilement configurer des nombreuses alertes activées selon des conditions de journal d’événements d’activité spécifiques dans le cadre de votre processus de déploiement automatisé.

les étapes de base Hello sont :

1. Créer un modèle en tant qu’un fichier JSON qui décrit comment activité de hello toocreate du journal d’alerte.

2. Déployer le modèle de hello à l’aide de [n’importe quelle méthode de déploiement](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Modèle Resource Manager pour une alerte de journal d’activité
toocreate une alerte de journal d’activité à l’aide d’un modèle de gestionnaire de ressources, vous créez une ressource de type de hello `microsoft.insights/activityLogAlerts`. Puis, renseignez toutes les propriétés associées. Voici un modèle qui crée une alerte de journal d’activité.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

Visitez notre [galerie Azure Quickstart](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) pour obtenir des exemples de modèle d’alertes du journal d’activité.

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur les [alertes](monitoring-overview-alerts.md).
- Découvrez comment tooadd [groupes d’actions à l’aide d’un modèle de gestionnaire de ressources](monitoring-create-action-group-with-resource-manager-template.md).
- Découvrez comment trop[créer un toomonitor alerte du journal des activités de toutes les opérations du moteur de mise à l’échelle de votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Découvrez comment trop[créer un toomonitor alerte du journal des activités toutes les opérations de montée/échelle Échec de mise à l’échelle de votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
