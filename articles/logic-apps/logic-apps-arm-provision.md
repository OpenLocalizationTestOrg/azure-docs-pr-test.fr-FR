---
title: "aaaCreate une application logique à l’aide d’un modèle dans Azure | Documents Microsoft"
description: "Utilisez un toodeploy de modèle Azure Resource Manager une application logique pour la définition de flux de travail."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a>Créer une application logique à l'aide d'un modèle
Les modèles fournissent un moyen rapide de toouse connecteurs différents au sein d’une application logique. Les applications de logique comprend des modèles Azure Resource Manager pour toocreate une application de la logique qui peut être utilisé toodefine des flux de travail. Vous pouvez définir quelles ressources sont déployées et la manière dont les paramètres toodefine lorsque vous déployez votre application logique. Vous pouvez utiliser ce modèle pour vos propres scénarios d’entreprise, ou personnaliser toomeet vos besoins.

Pour plus d’informations sur les propriétés de l’application hello logique, consultez [API de gestion des flux de travail logique d’application](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Pour obtenir des exemples de définition de hello proprement dite, consultez [définitions d’application logique d’auteur](logic-apps-author-definitions.md). 

Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Pour le modèle complète de hello, consultez [modèle d’application logique](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>Que déployer ?
Avec ce modèle, vous déployez une application logique.

déploiement de hello toorun sélectionner automatiquement, hello suivant bouton :  

[![Déployer tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>Paramètres
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Ressources toodeploy
### <a name="logic-app"></a>Application logique
Crée l’application logique de hello.

modèles de Hello utilise une valeur de paramètre pour le nom de l’application hello logique. Il définit l’emplacement hello de hello logique application toohello même emplacement que le groupe de ressources hello. 

Cette définition spécifique s’exécute une fois par heure et les tests ping hello emplacement spécifié dans hello **testUri** paramètre. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
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
      }
    }


## <a name="commands-toorun-deployment"></a>Déploiement de toorun de commandes
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interface de ligne de commande Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



