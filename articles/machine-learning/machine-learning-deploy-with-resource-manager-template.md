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
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="24843-103">Déployer un espace de travail Machine Learning à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="24843-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="24843-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="24843-104">Introduction</span></span>
<span data-ttu-id="24843-105">Temps en vous donnant une toodeploy évolutive qui soit à l’aide d’un modèle de déploiement vous évite de Azure Resource Manager interconnectés des composants avec un mécanisme de validation, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="24843-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="24843-106">tooset des espaces de travail Azure Machine Learning, par exemple, vous devez configurer un compte de stockage Azure de toofirst et déployez-le sur votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="24843-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="24843-107">Imaginez effectuer cette opération manuellement pour des centaines d’espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="24843-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="24843-108">Une alternative plus simple est toouse un toodeploy de modèle Azure Resource Manager un espace de travail Azure Machine Learning et toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="24843-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="24843-109">Cet article vous accompagne tout au long de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="24843-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="24843-110">Pour une intéressante présentation d’Azure Resource Manager, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24843-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="24843-111">Pas à pas : créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="24843-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="24843-112">Nous créerons un groupe de ressources Azure, puis déploierons un nouveau compte de stockage Azure et un nouvel espace de travail Azure Machine Learning à l’aide d’un modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24843-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="24843-113">Une fois le déploiement de hello est terminé, nous imprime des informations importantes sur les espaces de travail hello qui ont été créés (clé primaire de hello hello Id_espace_de_travail et espace de travail toohello hello URL).</span><span class="sxs-lookup"><span data-stu-id="24843-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="24843-114">Créer un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="24843-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="24843-115">Un espace de travail Machine Learning requiert un tooit dataset lié de stockage Azure compte toostore hello.</span><span class="sxs-lookup"><span data-stu-id="24843-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="24843-116">Hello modèle suivant utilise hello nom hello nom groupe de ressources toogenerate hello stockage compte et le nom d’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="24843-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="24843-117">Il utilise également nom de compte de stockage hello en tant que propriété lors de la création d’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="24843-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

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
<span data-ttu-id="24843-118">Enregistrez ce modèle en tant que fichier mlworkspace.json sous C:\temp\.</span><span class="sxs-lookup"><span data-stu-id="24843-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="24843-119">Déployer le groupe de ressources hello, basé sur le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="24843-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="24843-120">Ouvrez PowerShell</span><span class="sxs-lookup"><span data-stu-id="24843-120">Open PowerShell</span></span>
* <span data-ttu-id="24843-121">Installez les modules d’Azure Resource Manager et d’Azure Service Management</span><span class="sxs-lookup"><span data-stu-id="24843-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="24843-122">Ces étapes téléchargement et installez les étapes restantes de hello modules nécessaires toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="24843-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="24843-123">Cette opération ne doit toobe effectuée une seule fois dans un environnement hello où vous exécutez des commandes PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="24843-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="24843-124">Authentifier tooAzure</span><span class="sxs-lookup"><span data-stu-id="24843-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="24843-125">Cette étape doit toobe répété pour chaque session.</span><span class="sxs-lookup"><span data-stu-id="24843-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="24843-126">Une fois que vous êtes authentifié, vos informations d’abonnement s’affichent.</span><span class="sxs-lookup"><span data-stu-id="24843-126">Once authenticated, your subscription information should be displayed.</span></span>

![Compte Azure.][1]

<span data-ttu-id="24843-128">Maintenant que nous avons accès tooAzure, nous pouvons créer le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="24843-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="24843-129">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="24843-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="24843-130">Vérifier que ce groupe de ressources hello est correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="24843-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="24843-131">**ProvisioningState** doit être « Réussi ».</span><span class="sxs-lookup"><span data-stu-id="24843-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="24843-132">nom de groupe de ressources Hello est utilisé par le nom de compte de stockage hello modèle toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="24843-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="24843-133">nom de compte de stockage Hello doit être comprise entre 3 et 24 caractères et utiliser des nombres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="24843-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Groupe de ressources][2]

* <span data-ttu-id="24843-135">Déploiement de groupe de ressources hello, de déployer un nouvel espace de travail de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="24843-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="24843-136">Une fois le déploiement de hello est terminé, il est simple tooaccess des propriétés de l’espace de travail hello que vous avez déployé.</span><span class="sxs-lookup"><span data-stu-id="24843-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="24843-137">Par exemple, vous pouvez accéder à un jeton de clé primaire de hello.</span><span class="sxs-lookup"><span data-stu-id="24843-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="24843-138">Les jetons tooretrieve un autre moyen de l’espace de travail existant est toouse hello Invoke-AzureRmResourceAction commande.</span><span class="sxs-lookup"><span data-stu-id="24843-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="24843-139">Par exemple, vous pouvez répertorier les jetons principaux et secondaires de hello de tous les espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="24843-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="24843-140">Une fois que l’espace de travail hello est configuré, vous pouvez également automatiser plusieurs tâches d’Azure Machine Learning Studio à l’aide de hello [PowerShell Module pour Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="24843-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="24843-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24843-141">Next Steps</span></span>
* <span data-ttu-id="24843-142">Pour en savoir plus, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="24843-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="24843-143">Regardez hello [référentiel de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="24843-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="24843-144">Regardez cette vidéo sur [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="24843-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
