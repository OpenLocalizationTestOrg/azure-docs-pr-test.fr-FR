---
title: groupes de ressources aaaDeploy ressources Azure toomultiple | Documents Microsoft
description: "Montre comment tootarget plus de ressources Azure un groupe pendant le déploiement."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Déployer toomore de ressources Azure à un groupe de ressources

En général, vous déployez toutes les ressources hello dans votre modèle tooa seul groupe de ressources. Toutefois, il existe des scénarios où vous souhaitez toodeploy un ensemble de ressources ensemble, mais les placez dans différents groupes de ressources. Par exemple, vous souhaiterez toodeploy hello sauvegarde virtual machine pour l’emplacement et le groupe de ressources distinct tooa Azure Site Recovery. Le Gestionnaire de ressources vous permet de toouse imbriquée modèles tootarget différents groupes de ressources à un groupe de ressources hello utilisé pour le modèle de hello parent.

groupe de ressources Hello est le conteneur de cycle de vie hello pour une application hello et sa collection de ressources. Vous créez le groupe de ressources hello en dehors du modèle de hello et que vous spécifiez tootarget de groupe de ressources hello lors du déploiement. Pour un tooresource les groupes de présentation, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).

## <a name="example-template"></a>Exemple de modèle

tootarget une autre ressource, vous devez utiliser un modèle imbriqué ou lié au cours du déploiement. Hello `Microsoft.Resources/deployments` type de ressource offre un `resourceGroup` paramètre qui permet de vous toospecify un autre groupe de ressources pour hello imbriqués de déploiement. Tous les groupes de ressources hello doivent exister avant d’exécuter le déploiement de hello. exemple Hello déploie deux comptes de stockage - un dans le groupe de ressources hello spécifié pendant le déploiement et l’autre dans un groupe de ressources nommé `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

Si vous définissez `resourceGroup` toohello le nom d’un groupe de ressources qui n’existe pas, le déploiement du hello échoue. Si vous ne fournissez pas de valeur pour `resourceGroup`, Gestionnaire de ressources utilise le groupe de ressources parent hello.  

## <a name="deploy-hello-template"></a>Déployer le modèle de hello

toodeploy hello exemple de modèle que vous pouvez utiliser le portail de hello, Azure PowerShell ou CLI d’Azure. Pour Azure PowerShell ou d’Azure CLI, vous devez utiliser une version postérieure au mois d’avril 2017. les exemples Hello supposent que vous avez enregistré le modèle de hello localement en tant qu’un fichier nommé **crossrgdeployment.json**.

Pour PowerShell :

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Pour Azure CLI :

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

Une fois le déploiement terminé, deux groupes de ressources s’affichent. Chaque groupe de ressources contient un compte de stockage.

## <a name="use-resourcegroup-function"></a>Utiliser la fonction resourceGroup()

Pour franchir les déploiements de groupe de ressources, hello [resouceGroup() fonction](resource-group-template-functions-resource.md#resourcegroup) résout différemment selon la façon dont vous spécifiez les modèles imbriqués hello. 

Si vous incorporez un modèle dans un autre modèle, resouceGroup() dans les modèles imbriqués hello résout groupe de ressources toohello parent. Un modèle incorporé utilise hello suivant le format :

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

Si vous liez le modèle séparé de tooa, resouceGroup() dans le modèle lié de hello résout groupe de ressources imbriquées toohello. Un modèle lié utilise hello suivant le format :

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>Étapes suivantes

* toounderstand toodefine des paramètres dans votre modèle, voir [comprendre la structure de hello et syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).
* Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).
