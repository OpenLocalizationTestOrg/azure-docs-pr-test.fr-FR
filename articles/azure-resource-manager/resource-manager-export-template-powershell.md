---
title: "Exporter un modèle Azure Resource Manager avec Azure PowerShell| Microsoft Docs"
description: "Utilisez Azure Resource Manager et Azure PowerShell pour exporter un modèle à partir d’un groupe de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 7543811eb9448222b6e7c266756e68debc7d54be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="8661a-103">Exporter des modèles Azure Resource Manager avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="8661a-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="8661a-104">Resource Manager vous permet d’exporter un modèle Resource Manager à partir de ressources existantes de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8661a-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="8661a-105">Vous pouvez utiliser le modèle généré pour découvrir la syntaxe du modèle, ou pour automatiser le redéploiement de votre solution en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="8661a-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="8661a-106">Il est important de noter qu’il existe deux façons différentes d’exporter un modèle :</span><span class="sxs-lookup"><span data-stu-id="8661a-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="8661a-107">Vous pouvez exporter le modèle actuel que vous avez utilisé pour un déploiement.</span><span class="sxs-lookup"><span data-stu-id="8661a-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="8661a-108">Le modèle exporté inclut l’ensemble des paramètres et des variables exactement comme ils apparaissent dans le modèle d’origine.</span><span class="sxs-lookup"><span data-stu-id="8661a-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="8661a-109">Cette approche est utile lorsque vous avez besoin de récupérer un modèle.</span><span class="sxs-lookup"><span data-stu-id="8661a-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="8661a-110">Vous pouvez exporter le modèle qui représente l’état actuel du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8661a-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="8661a-111">Le modèle exporté n’est pas basé sur un modèle utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8661a-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="8661a-112">Au lieu de cela, il crée un modèle qui est un instantané du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8661a-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="8661a-113">Le modèle exporté a probablement de nombreuses valeurs codées en dur et pas autant de paramètres que vous pourriez généralement définir.</span><span class="sxs-lookup"><span data-stu-id="8661a-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="8661a-114">Cette approche est utile lorsque vous avez modifié le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8661a-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="8661a-115">Vous devez maintenant capturer le groupe de ressources en tant que modèle.</span><span class="sxs-lookup"><span data-stu-id="8661a-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="8661a-116">Cette rubrique illustre les deux approches.</span><span class="sxs-lookup"><span data-stu-id="8661a-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="8661a-117">Déployer une solution</span><span class="sxs-lookup"><span data-stu-id="8661a-117">Deploy a solution</span></span>

<span data-ttu-id="8661a-118">Afin d’illustrer ces deux approches pour l’exportation d’un modèle, commençons par le déploiement d’une solution dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8661a-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="8661a-119">Si vous disposez déjà d’un groupe de ressources dans votre abonnement que vous voulez exporter, il est inutile de déployer cette solution.</span><span class="sxs-lookup"><span data-stu-id="8661a-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="8661a-120">Toutefois, le reste de cet article fait référence au modèle pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="8661a-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="8661a-121">L’exemple de script déploie un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8661a-121">The example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="8661a-122">Enregistrer un modèle à partir de l’historique de déploiement</span><span class="sxs-lookup"><span data-stu-id="8661a-122">Save template from deployment history</span></span>

<span data-ttu-id="8661a-123">Vous pouvez récupérer un modèle à partir de votre historique de déploiement à l’aide de la commande [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate).</span><span class="sxs-lookup"><span data-stu-id="8661a-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="8661a-124">L’exemple suivant enregistre le modèle que vous déployez précédemment :</span><span class="sxs-lookup"><span data-stu-id="8661a-124">The following example saves the template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="8661a-125">Il renvoie l’emplacement du modèle.</span><span class="sxs-lookup"><span data-stu-id="8661a-125">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="8661a-126">Ouvrez le fichier et notez qu’il s’agit exactement du même modèle que celui que vous avez utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8661a-126">Open the file, and notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="8661a-127">Les paramètres et les variables correspondent au modèle provenant de GitHub.</span><span class="sxs-lookup"><span data-stu-id="8661a-127">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="8661a-128">Vous pouvez redéployer ce modèle.</span><span class="sxs-lookup"><span data-stu-id="8661a-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="8661a-129">Exporter un groupe de ressources en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="8661a-129">Export resource group as template</span></span>

<span data-ttu-id="8661a-130">Au lieu de récupérer un modèle à partir de l’historique de déploiement, vous pouvez récupérer un modèle qui représente l’état actuel d’un groupe de ressources à l’aide de la commande [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8661a-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="8661a-131">Vous utilisez cette commande lorsque vous avez effectué de nombreuses modifications dans votre groupe de ressources et qu’aucun modèle existant ne représente toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="8661a-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="8661a-132">Il renvoie l’emplacement du modèle.</span><span class="sxs-lookup"><span data-stu-id="8661a-132">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="8661a-133">Ouvrez le fichier et notez qu’il est différent de celui du modèle dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="8661a-133">Open the file, and notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="8661a-134">Il a des paramètres différents et aucune variable.</span><span class="sxs-lookup"><span data-stu-id="8661a-134">It has different parameters and no variables.</span></span> <span data-ttu-id="8661a-135">La référence (SKU) de stockage et l’emplacement sont codés en dur dans des valeurs.</span><span class="sxs-lookup"><span data-stu-id="8661a-135">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="8661a-136">L’exemple suivant montre le modèle exporté, mais votre modèle a un nom de paramètre légèrement différent :</span><span class="sxs-lookup"><span data-stu-id="8661a-136">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="8661a-137">Vous pouvez redéployer ce modèle, mais cela requiert de deviner un nom unique pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8661a-137">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="8661a-138">Le nom de votre paramètre est légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="8661a-138">The name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="8661a-139">Personnaliser un modèle exporté</span><span class="sxs-lookup"><span data-stu-id="8661a-139">Customize exported template</span></span>

<span data-ttu-id="8661a-140">Vous pouvez modifier ce modèle pour le rendre plus facile à utiliser et plus flexible.</span><span class="sxs-lookup"><span data-stu-id="8661a-140">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="8661a-141">Pour autoriser plusieurs emplacements, modifiez la propriété d’emplacement de façon à utiliser le même emplacement que le groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="8661a-141">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="8661a-142">Pour éviter d’avoir à deviner un nom unique pour le compte de stockage, supprimez le paramètre pour le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8661a-142">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="8661a-143">Ajoutez un paramètre pour un suffixe de nom de stockage et une référence (SKU) de stockage :</span><span class="sxs-lookup"><span data-stu-id="8661a-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="8661a-144">Ajoutez une variable qui construit le nom du compte de stockage avec la fonction uniqueString :</span><span class="sxs-lookup"><span data-stu-id="8661a-144">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="8661a-145">Définissez le nom du compte de stockage sur la variable :</span><span class="sxs-lookup"><span data-stu-id="8661a-145">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="8661a-146">Définissez la référence SKU sur le paramètre :</span><span class="sxs-lookup"><span data-stu-id="8661a-146">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="8661a-147">Votre modèle doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="8661a-147">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="8661a-148">Redéployez le modèle modifié.</span><span class="sxs-lookup"><span data-stu-id="8661a-148">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8661a-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8661a-149">Next steps</span></span>
* <span data-ttu-id="8661a-150">Pour plus d’informations sur l’utilisation du portail pour exporter un modèle, voir [Exporter un modèle Azure Resource Manager à partir de ressources existantes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="8661a-150">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="8661a-151">Pour définir des paramètres dans le modèle, consultez [Création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="8661a-151">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="8661a-152">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="8661a-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
