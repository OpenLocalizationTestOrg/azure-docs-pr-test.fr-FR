---
title: aaaDeploy un espace de travail Machine Learning avec Azure Resource Manager | Documents Microsoft
description: "Comment toodeploy un espace de travail pour l’apprentissage d’Azure à l’aide du modèle Azure Resource Manager"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Déployer un espace de travail Machine Learning à l’aide d’Azure Resource Manager
## <a name="introduction"></a>Introduction
Temps en vous donnant une toodeploy évolutive qui soit à l’aide d’un modèle de déploiement vous évite de Azure Resource Manager interconnectés des composants avec un mécanisme de validation, puis réessayez. tooset des espaces de travail Azure Machine Learning, par exemple, vous devez configurer un compte de stockage Azure de toofirst et déployez-le sur votre espace de travail. Imaginez effectuer cette opération manuellement pour des centaines d’espaces de travail. Une alternative plus simple est toouse un toodeploy de modèle Azure Resource Manager un espace de travail Azure Machine Learning et toutes ses dépendances. Cet article vous accompagne tout au long de cette procédure pas à pas. Pour une intéressante présentation d’Azure Resource Manager, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Pas à pas : créer un espace de travail Machine Learning
Nous créerons un groupe de ressources Azure, puis déploierons un nouveau compte de stockage Azure et un nouvel espace de travail Azure Machine Learning à l’aide d’un modèle Resource Manager. Une fois le déploiement de hello est terminé, nous imprime des informations importantes sur les espaces de travail hello qui ont été créés (clé primaire de hello hello Id_espace_de_travail et espace de travail toohello hello URL).

### <a name="create-an-azure-resource-manager-template"></a>Créer un modèle Azure Resource Manager
Un espace de travail Machine Learning requiert un tooit dataset lié de stockage Azure compte toostore hello.
Hello modèle suivant utilise hello nom hello nom groupe de ressources toogenerate hello stockage compte et le nom d’espace de travail hello.  Il utilise également nom de compte de stockage hello en tant que propriété lors de la création d’espace de travail hello.

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
Enregistrez ce modèle en tant que fichier mlworkspace.json sous C:\temp\.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Déployer le groupe de ressources hello, basé sur le modèle de hello
* Ouvrez PowerShell
* Installez les modules d’Azure Resource Manager et d’Azure Service Management  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Ces étapes téléchargement et installez les étapes restantes de hello modules nécessaires toocomplete hello. Cette opération ne doit toobe effectuée une seule fois dans un environnement hello où vous exécutez des commandes PowerShell de hello.   

* Authentifier tooAzure  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Cette étape doit toobe répété pour chaque session. Une fois que vous êtes authentifié, vos informations d’abonnement s’affichent.

![Compte Azure.][1]

Maintenant que nous avons accès tooAzure, nous pouvons créer le groupe de ressources hello.

* Créer un groupe de ressources

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Vérifier que ce groupe de ressources hello est correctement configuré. **ProvisioningState** doit être « Réussi ».
nom de groupe de ressources Hello est utilisé par le nom de compte de stockage hello modèle toogenerate hello. nom de compte de stockage Hello doit être comprise entre 3 et 24 caractères et utiliser des nombres et des lettres minuscules.

![Groupe de ressources][2]

* Déploiement de groupe de ressources hello, de déployer un nouvel espace de travail de Machine Learning.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Une fois le déploiement de hello est terminé, il est simple tooaccess des propriétés de l’espace de travail hello que vous avez déployé. Par exemple, vous pouvez accéder à un jeton de clé primaire de hello.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Les jetons tooretrieve un autre moyen de l’espace de travail existant est toouse hello Invoke-AzureRmResourceAction commande. Par exemple, vous pouvez répertorier les jetons principaux et secondaires de hello de tous les espaces de travail.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Une fois que l’espace de travail hello est configuré, vous pouvez également automatiser plusieurs tâches d’Azure Machine Learning Studio à l’aide de hello [PowerShell Module pour Azure Machine Learning](http://aka.ms/amlps).

## <a name="next-steps"></a>Étapes suivantes
* Pour en savoir plus, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). 
* Regardez hello [référentiel de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates). 
* Regardez cette vidéo sur [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
