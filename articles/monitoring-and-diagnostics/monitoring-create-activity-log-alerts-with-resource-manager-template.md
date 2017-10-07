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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="e3070-103">Créer une alerte de journal d’activité avec un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3070-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="e3070-104">Cet article vous explique comment toouse un [modèle Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) alertes de journal d’activité tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="e3070-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="e3070-105">À l’aide de modèles, vous pouvez facilement configurer des nombreuses alertes activées selon des conditions de journal d’événements d’activité spécifiques dans le cadre de votre processus de déploiement automatisé.</span><span class="sxs-lookup"><span data-stu-id="e3070-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="e3070-106">les étapes de base Hello sont :</span><span class="sxs-lookup"><span data-stu-id="e3070-106">hello basic steps are:</span></span>

1. <span data-ttu-id="e3070-107">Créer un modèle en tant qu’un fichier JSON qui décrit comment activité de hello toocreate du journal d’alerte.</span><span class="sxs-lookup"><span data-stu-id="e3070-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="e3070-108">Déployer le modèle de hello à l’aide de [n’importe quelle méthode de déploiement](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="e3070-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="e3070-109">Modèle Resource Manager pour une alerte de journal d’activité</span><span class="sxs-lookup"><span data-stu-id="e3070-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="e3070-110">toocreate une alerte de journal d’activité à l’aide d’un modèle de gestionnaire de ressources, vous créez une ressource de type de hello `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="e3070-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="e3070-111">Puis, renseignez toutes les propriétés associées.</span><span class="sxs-lookup"><span data-stu-id="e3070-111">Then you fill in all related properties.</span></span> <span data-ttu-id="e3070-112">Voici un modèle qui crée une alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="e3070-112">Here's a template that creates an activity log alert.</span></span>

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

<span data-ttu-id="e3070-113">Visitez notre [galerie Azure Quickstart](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) pour obtenir des exemples de modèle d’alertes du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="e3070-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3070-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3070-114">Next steps</span></span>
- <span data-ttu-id="e3070-115">En savoir plus sur les [alertes](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e3070-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="e3070-116">Découvrez comment tooadd [groupes d’actions à l’aide d’un modèle de gestionnaire de ressources](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e3070-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="e3070-117">Découvrez comment trop[créer un toomonitor alerte du journal des activités de toutes les opérations du moteur de mise à l’échelle de votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="e3070-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="e3070-118">Découvrez comment trop[créer un toomonitor alerte du journal des activités toutes les opérations de montée/échelle Échec de mise à l’échelle de votre abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="e3070-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
