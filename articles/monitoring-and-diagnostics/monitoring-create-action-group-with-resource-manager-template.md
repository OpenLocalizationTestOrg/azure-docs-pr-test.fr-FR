---
title: "groupes d’actions aaaCreate avec modèles Resource Manager | Documents Microsoft"
description: "Découvrez comment toocreate une action de groupe à l’aide d’un modèle Azure Resource Manager."
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
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="8098e-103">Créer un groupe d’actions avec un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8098e-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="8098e-104">Cet article vous explique comment toouse un [modèle Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure groupes d’actions.</span><span class="sxs-lookup"><span data-stu-id="8098e-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="8098e-105">À l’aide de modèles, vous pouvez configurer automatiquement des groupes d’actions qui peuvent être réutilisés dans certains types d’alertes.</span><span class="sxs-lookup"><span data-stu-id="8098e-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="8098e-106">Ces groupes d’actions vous assurer que tous les hello correct parties sont avertis lorsqu’une alerte est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="8098e-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="8098e-107">les étapes de base Hello sont :</span><span class="sxs-lookup"><span data-stu-id="8098e-107">hello basic steps are:</span></span>

1. <span data-ttu-id="8098e-108">Créer un modèle en tant qu’un fichier JSON qui décrit comment toocreate hello groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="8098e-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="8098e-109">Déployer le modèle de hello à l’aide de [n’importe quelle méthode de déploiement](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="8098e-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="8098e-110">Tout d’abord, nous allons décrire comment toocreate un modèle de gestionnaire de ressources pour une action de groupe dans lequel les définitions d’action hello sont codés en dur dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="8098e-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="8098e-111">Ensuite, nous décrivons comment toocreate un modèle qui prend les informations de configuration de webhook hello en tant que paramètres d’entrée lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="8098e-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="8098e-112">Modèles Resource Manager pour un groupe d’actions</span><span class="sxs-lookup"><span data-stu-id="8098e-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="8098e-113">toocreate un groupe d’actions à l’aide d’un modèle de gestionnaire de ressources, vous créez une ressource de type de hello `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="8098e-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="8098e-114">Puis, renseignez toutes les propriétés associées.</span><span class="sxs-lookup"><span data-stu-id="8098e-114">Then you fill in all related properties.</span></span> <span data-ttu-id="8098e-115">Voici deux exemples de modèles qui créent un groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="8098e-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
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
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
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


## <a name="next-steps"></a><span data-ttu-id="8098e-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8098e-116">Next steps</span></span>
* <span data-ttu-id="8098e-117">En savoir plus sur les [groupes d’actions](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8098e-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="8098e-118">En savoir plus sur les [alertes](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8098e-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="8098e-119">Découvrez comment tooadd [alertes à l’aide d’un modèle de gestionnaire de ressources](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8098e-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
