---
title: "Déployer des ressources Azure sur plusieurs groupes de ressources | Microsoft Docs"
description: "Montre comment cibler plusieurs groupes de ressources Azure pendant le déploiement."
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
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="98ea4-103">Déployer des ressources Azure sur plusieurs groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="98ea4-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="98ea4-104">En général, vous déployez toutes les ressources dans votre modèle sur un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="98ea4-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="98ea4-105">Toutefois, il existe des scénarios dans lesquels vous souhaitez déployer simultanément un ensemble de ressources à placer dans différents groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="98ea4-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="98ea4-106">Par exemple, vous voudrez peut-être déployer la machine virtuelle de sauvegarde destinée à Azure Site Recovery sur un groupe de ressources et un emplacement distincts.</span><span class="sxs-lookup"><span data-stu-id="98ea4-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="98ea4-107">Resource Manager vous permet d’utiliser des modèles imbriqués pour cibler des groupes de ressources différents de celui utilisé pour le modèle parent.</span><span class="sxs-lookup"><span data-stu-id="98ea4-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="98ea4-108">Le groupe de ressources est le conteneur de cycle de vie de l’application et sa collection de ressources.</span><span class="sxs-lookup"><span data-stu-id="98ea4-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="98ea4-109">Vous créez le groupe de ressources en dehors du modèle et spécifiez le groupe de ressources à cibler lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="98ea4-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="98ea4-110">Pour voir une présentation des groupes de ressources, consultez la page [Présentation d’Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98ea4-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="98ea4-111">Exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="98ea4-111">Example template</span></span>

<span data-ttu-id="98ea4-112">Pour cibler une autre ressource, vous devez utiliser un modèle imbriqué ou lié au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="98ea4-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="98ea4-113">Le type de ressource `Microsoft.Resources/deployments` fournit un paramètre `resourceGroup` qui vous permet de spécifier un autre groupe de ressources pour le déploiement imbriqué.</span><span class="sxs-lookup"><span data-stu-id="98ea4-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="98ea4-114">Tous les groupes de ressources doivent exister avant l’exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="98ea4-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="98ea4-115">L’exemple suivant déploie deux comptes de stockage, un dans le groupe de ressources spécifié pendant le déploiement et l’autre dans un groupe de ressources nommé `crossResourceGroupDeployment` :</span><span class="sxs-lookup"><span data-stu-id="98ea4-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="98ea4-116">Si vous définissez `resourceGroup`sur le nom d’un groupe de ressources qui n’existe pas, le déploiement échoue.</span><span class="sxs-lookup"><span data-stu-id="98ea4-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="98ea4-117">Si vous n’indiquez pas de valeur pour `resourceGroup`, Resource Manager utilise le groupe de ressources parent.</span><span class="sxs-lookup"><span data-stu-id="98ea4-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="98ea4-118">Déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="98ea4-118">Deploy the template</span></span>

<span data-ttu-id="98ea4-119">Pour déployer l’exemple de modèle, vous pouvez utiliser le portail, Azure PowerShell ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="98ea4-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="98ea4-120">Pour Azure PowerShell ou d’Azure CLI, vous devez utiliser une version postérieure au mois d’avril 2017.</span><span class="sxs-lookup"><span data-stu-id="98ea4-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="98ea4-121">Les exemples supposent que vous avez enregistré le modèle localement dans un fichier nommé **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="98ea4-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="98ea4-122">Pour PowerShell :</span><span class="sxs-lookup"><span data-stu-id="98ea4-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="98ea4-123">Pour Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="98ea4-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="98ea4-124">Une fois le déploiement terminé, deux groupes de ressources s’affichent.</span><span class="sxs-lookup"><span data-stu-id="98ea4-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="98ea4-125">Chaque groupe de ressources contient un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="98ea4-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="98ea4-126">Utiliser la fonction resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="98ea4-126">Use resourceGroup() function</span></span>

<span data-ttu-id="98ea4-127">Pour des déploiements entre groupes de ressources, la [fonction resouceGroup()](resource-group-template-functions-resource.md#resourcegroup) produit un résultat différent selon la façon dont vous spécifiez le modèle imbriqué.</span><span class="sxs-lookup"><span data-stu-id="98ea4-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="98ea4-128">Si vous incorporez un modèle dans un autre, la résolution de resouceGroup() dans le modèle imbriqué est le groupe de ressources parent.</span><span class="sxs-lookup"><span data-stu-id="98ea4-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="98ea4-129">Un modèle incorporé utilise le format suivant :</span><span class="sxs-lookup"><span data-stu-id="98ea4-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="98ea4-130">Si vous liez à un modèle séparé, la résolution de resouceGroup() dans le modèle lié est le groupe de ressources imbriqué.</span><span class="sxs-lookup"><span data-stu-id="98ea4-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="98ea4-131">Un modèle lié utilise le format suivant :</span><span class="sxs-lookup"><span data-stu-id="98ea4-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="98ea4-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98ea4-132">Next steps</span></span>

* <span data-ttu-id="98ea4-133">Pour comprendre comment définir des paramètres dans votre modèle, consultez [Comprendre la structure et la syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="98ea4-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="98ea4-134">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="98ea4-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="98ea4-135">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="98ea4-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
