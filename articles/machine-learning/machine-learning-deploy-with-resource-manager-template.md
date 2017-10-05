---
title: "Déployer un espace de travail Machine Learning avec Azure Resource Manager | Microsoft Docs"
description: "Comment déployer un espace de travail pour Azure Machine Learning à l’aide du modèle Azure Resource Manager"
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
ms.openlocfilehash: 9e37780428b0867da63987ec4f7f843a8abeb907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="39b89-103">Déployer un espace de travail Machine Learning à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="39b89-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="39b89-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="39b89-104">Introduction</span></span>
<span data-ttu-id="39b89-105">Les modèles de déploiement Azure Resource Manager vous font gagner du temps en vous offrant une méthode évolutive pour déployer des composants interconnectés avec un mécanisme de validation et de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="39b89-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="39b89-106">Pour configurer des espaces de travail Azure Machine Learning, par exemple, vous devez d’abord configurer un compte de stockage Azure et ensuite déployer votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="39b89-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="39b89-107">Imaginez effectuer cette opération manuellement pour des centaines d’espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="39b89-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="39b89-108">Une alternative plus simple consiste à utiliser un modèle Azure Resource Manager pour déployer un espace de travail Azure Machine Learning et toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="39b89-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="39b89-109">Cet article vous accompagne tout au long de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="39b89-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="39b89-110">Pour une intéressante présentation d’Azure Resource Manager, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39b89-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="39b89-111">Pas à pas : créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="39b89-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="39b89-112">Nous créerons un groupe de ressources Azure, puis déploierons un nouveau compte de stockage Azure et un nouvel espace de travail Azure Machine Learning à l’aide d’un modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39b89-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="39b89-113">Une fois le déploiement terminé, nous imprimerons des informations importantes sur les espaces de travail créés (clé primaire, workspaceID et URL de l’espace de travail).</span><span class="sxs-lookup"><span data-stu-id="39b89-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="39b89-114">Créer un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="39b89-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="39b89-115">Un espace de travail Machine Learning requiert un compte de stockage Azure pour stocker le jeu de données lié.</span><span class="sxs-lookup"><span data-stu-id="39b89-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="39b89-116">Le modèle suivant utilise le nom du groupe de ressources pour générer le nom du compte de stockage et celui de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="39b89-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="39b89-117">Il utilise également le nom du compte de stockage comme propriété lors de la création de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="39b89-117">It also uses the storage account name as a property when creating the workspace.</span></span>

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
<span data-ttu-id="39b89-118">Enregistrez ce modèle en tant que fichier mlworkspace.json sous C:\temp\.</span><span class="sxs-lookup"><span data-stu-id="39b89-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="39b89-119">Déployer le groupe de ressources à partir du modèle</span><span class="sxs-lookup"><span data-stu-id="39b89-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="39b89-120">Ouvrez PowerShell</span><span class="sxs-lookup"><span data-stu-id="39b89-120">Open PowerShell</span></span>
* <span data-ttu-id="39b89-121">Installez les modules d’Azure Resource Manager et d’Azure Service Management</span><span class="sxs-lookup"><span data-stu-id="39b89-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="39b89-122">Ces étapes de téléchargement et d’installation des modules sont nécessaires pour effectuer les étapes restantes.</span><span class="sxs-lookup"><span data-stu-id="39b89-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="39b89-123">Cette opération ne doit être effectuée qu’une fois dans l’environnement dans lequel vous exécutez les commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39b89-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="39b89-124">Authentifiez-vous sur Azure</span><span class="sxs-lookup"><span data-stu-id="39b89-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="39b89-125">Cette étape doit être répétée pour chaque session.</span><span class="sxs-lookup"><span data-stu-id="39b89-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="39b89-126">Une fois que vous êtes authentifié, vos informations d’abonnement s’affichent.</span><span class="sxs-lookup"><span data-stu-id="39b89-126">Once authenticated, your subscription information should be displayed.</span></span>

![Compte Azure.][1]

<span data-ttu-id="39b89-128">Maintenant que nous avons accès à Azure, nous pouvons créer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="39b89-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="39b89-129">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="39b89-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="39b89-130">Vérifiez que le groupe de ressources est correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="39b89-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="39b89-131">**ProvisioningState** doit être « Réussi ».</span><span class="sxs-lookup"><span data-stu-id="39b89-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="39b89-132">Le nom du groupe de ressources est utilisé par le modèle pour générer le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="39b89-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="39b89-133">Le nom du compte de stockage doit comprendre entre 3 et 24 caractères, uniquement des lettres en minuscules et des nombres.</span><span class="sxs-lookup"><span data-stu-id="39b89-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Groupe de ressources][2]

* <span data-ttu-id="39b89-135">À l’aide du déploiement du groupe de ressources, déployez un nouvel espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="39b89-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="39b89-136">Une fois le déploiement terminé, il est simple d’accéder aux propriétés de l’espace de travail que vous avez déployé.</span><span class="sxs-lookup"><span data-stu-id="39b89-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="39b89-137">Par exemple, vous pouvez accéder au jeton de clé primaire.</span><span class="sxs-lookup"><span data-stu-id="39b89-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="39b89-138">Une autre méthode pour récupérer des jetons de l’espace de travail existant consiste à utiliser la commande Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="39b89-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="39b89-139">Par exemple, vous pouvez répertorier les jetons principaux et secondaires de tous les espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="39b89-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="39b89-140">Après la configuration de l’espace de travail, vous pouvez également automatiser de nombreuses tâches Azure Machine Learning Studio à l’aide du [Module PowerShell pour Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="39b89-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39b89-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39b89-141">Next Steps</span></span>
* <span data-ttu-id="39b89-142">Pour en savoir plus, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="39b89-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="39b89-143">Parcourez le [Référentiel de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="39b89-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="39b89-144">Regardez cette vidéo sur [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="39b89-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
