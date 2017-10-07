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
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="1b254-103">Déployer toomore de ressources Azure à un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="1b254-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="1b254-104">En général, vous déployez toutes les ressources hello dans votre modèle tooa seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1b254-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="1b254-105">Toutefois, il existe des scénarios où vous souhaitez toodeploy un ensemble de ressources ensemble, mais les placez dans différents groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="1b254-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="1b254-106">Par exemple, vous souhaiterez toodeploy hello sauvegarde virtual machine pour l’emplacement et le groupe de ressources distinct tooa Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1b254-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="1b254-107">Le Gestionnaire de ressources vous permet de toouse imbriquée modèles tootarget différents groupes de ressources à un groupe de ressources hello utilisé pour le modèle de hello parent.</span><span class="sxs-lookup"><span data-stu-id="1b254-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="1b254-108">groupe de ressources Hello est le conteneur de cycle de vie hello pour une application hello et sa collection de ressources.</span><span class="sxs-lookup"><span data-stu-id="1b254-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="1b254-109">Vous créez le groupe de ressources hello en dehors du modèle de hello et que vous spécifiez tootarget de groupe de ressources hello lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="1b254-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="1b254-110">Pour un tooresource les groupes de présentation, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b254-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="1b254-111">Exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="1b254-111">Example template</span></span>

<span data-ttu-id="1b254-112">tootarget une autre ressource, vous devez utiliser un modèle imbriqué ou lié au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="1b254-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="1b254-113">Hello `Microsoft.Resources/deployments` type de ressource offre un `resourceGroup` paramètre qui permet de vous toospecify un autre groupe de ressources pour hello imbriqués de déploiement.</span><span class="sxs-lookup"><span data-stu-id="1b254-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="1b254-114">Tous les groupes de ressources hello doivent exister avant d’exécuter le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="1b254-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="1b254-115">exemple Hello déploie deux comptes de stockage - un dans le groupe de ressources hello spécifié pendant le déploiement et l’autre dans un groupe de ressources nommé `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="1b254-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="1b254-116">Si vous définissez `resourceGroup` toohello le nom d’un groupe de ressources qui n’existe pas, le déploiement du hello échoue.</span><span class="sxs-lookup"><span data-stu-id="1b254-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="1b254-117">Si vous ne fournissez pas de valeur pour `resourceGroup`, Gestionnaire de ressources utilise le groupe de ressources parent hello.</span><span class="sxs-lookup"><span data-stu-id="1b254-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="1b254-118">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="1b254-118">Deploy hello template</span></span>

<span data-ttu-id="1b254-119">toodeploy hello exemple de modèle que vous pouvez utiliser le portail de hello, Azure PowerShell ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1b254-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="1b254-120">Pour Azure PowerShell ou d’Azure CLI, vous devez utiliser une version postérieure au mois d’avril 2017.</span><span class="sxs-lookup"><span data-stu-id="1b254-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="1b254-121">les exemples Hello supposent que vous avez enregistré le modèle de hello localement en tant qu’un fichier nommé **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="1b254-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="1b254-122">Pour PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1b254-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="1b254-123">Pour Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="1b254-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="1b254-124">Une fois le déploiement terminé, deux groupes de ressources s’affichent.</span><span class="sxs-lookup"><span data-stu-id="1b254-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="1b254-125">Chaque groupe de ressources contient un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1b254-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="1b254-126">Utiliser la fonction resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="1b254-126">Use resourceGroup() function</span></span>

<span data-ttu-id="1b254-127">Pour franchir les déploiements de groupe de ressources, hello [resouceGroup() fonction](resource-group-template-functions-resource.md#resourcegroup) résout différemment selon la façon dont vous spécifiez les modèles imbriqués hello.</span><span class="sxs-lookup"><span data-stu-id="1b254-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="1b254-128">Si vous incorporez un modèle dans un autre modèle, resouceGroup() dans les modèles imbriqués hello résout groupe de ressources toohello parent.</span><span class="sxs-lookup"><span data-stu-id="1b254-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="1b254-129">Un modèle incorporé utilise hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="1b254-129">An embedded template uses hello following format:</span></span>

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

<span data-ttu-id="1b254-130">Si vous liez le modèle séparé de tooa, resouceGroup() dans le modèle lié de hello résout groupe de ressources imbriquées toohello.</span><span class="sxs-lookup"><span data-stu-id="1b254-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="1b254-131">Un modèle lié utilise hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="1b254-131">A linked template uses hello following format:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1b254-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b254-132">Next steps</span></span>

* <span data-ttu-id="1b254-133">toounderstand toodefine des paramètres dans votre modèle, voir [comprendre la structure de hello et syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1b254-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="1b254-134">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="1b254-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="1b254-135">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="1b254-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
