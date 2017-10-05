---
title: "Créer des groupes d’actions avec les modèles Resource Manager | Microsoft Docs"
description: "Découvrez comment créer un groupe d’actions à l’aide d’un modèle Azure Resource Manager."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 76bf353cac13f1c2169380f8dd3c1e163d4f3f41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="0ba28-103">Créer un groupe d’actions avec un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0ba28-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="0ba28-104">Cet article vous explique comment utiliser un [modèle Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) pour configurer les groupes d’action.</span><span class="sxs-lookup"><span data-stu-id="0ba28-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="0ba28-105">À l’aide de modèles, vous pouvez configurer automatiquement des groupes d’actions qui peuvent être réutilisés dans certains types d’alertes.</span><span class="sxs-lookup"><span data-stu-id="0ba28-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="0ba28-106">Ces groupes d’actions vous assurent que toutes les parties concernées sont averties lorsqu’une alerte est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="0ba28-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="0ba28-107">Étapes élémentaires :</span><span class="sxs-lookup"><span data-stu-id="0ba28-107">The basic steps are:</span></span>

1. <span data-ttu-id="0ba28-108">Créez un modèle sous la forme d’un fichier JSON qui décrit comment créer le groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="0ba28-108">Create a template as a JSON file that describes how to create the action group.</span></span>

2. <span data-ttu-id="0ba28-109">Déployez le modèle à l’aide de [n’importe quelle méthode de déploiement](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="0ba28-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="0ba28-110">Nous allons tout d’abord présenter comment créer un modèle Resource Manager pour un groupe d’actions où les définitions d’action sont codées en dur dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="0ba28-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span></span> <span data-ttu-id="0ba28-111">Nous allons ensuite expliquer comment créer un modèle qui utilise les informations de configuration de webhook comme des paramètres d’entrée lorsque le modèle est déployé.</span><span class="sxs-lookup"><span data-stu-id="0ba28-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="0ba28-112">Modèles Resource Manager pour un groupe d’actions</span><span class="sxs-lookup"><span data-stu-id="0ba28-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="0ba28-113">Pour créer un groupe d’actions à l’aide d’un modèle Resource Manager, vous créez une ressource de type `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="0ba28-113">To create an action group by using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="0ba28-114">Vous renseignez ensuite toutes les propriétés associées.</span><span class="sxs-lookup"><span data-stu-id="0ba28-114">Then you fill in all related properties.</span></span> <span data-ttu-id="0ba28-115">Voici deux exemples de modèles qui créent un groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="0ba28-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a><span data-ttu-id="0ba28-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ba28-116">Next steps</span></span>
* <span data-ttu-id="0ba28-117">En savoir plus sur les [groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="0ba28-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="0ba28-118">En savoir plus sur les [alertes](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0ba28-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="0ba28-119">En savoir pour sur l’ajout d’[alertes à l’aide d’un modèle Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="0ba28-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
