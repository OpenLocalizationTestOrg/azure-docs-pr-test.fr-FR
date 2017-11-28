---
title: "modèle de gestionnaire de ressources aaaExport avec Azure PowerShell | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et d’Azure PowerShell tooexport un modèle à partir d’un groupe de ressources."
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
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="a7722-103">Exporter des modèles Azure Resource Manager avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7722-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="a7722-104">Le Gestionnaire de ressources vous permet de tooexport un modèle de gestionnaire de ressources à partir de ressources existants dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7722-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="a7722-105">Vous pouvez utiliser ce toolearn modèle généré sur hello modèle syntaxe ou tooautomate hello redéploiement de votre solution en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="a7722-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="a7722-106">Il est important toonote qu’il existe deux façons différentes tooexport un modèle :</span><span class="sxs-lookup"><span data-stu-id="a7722-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="a7722-107">Vous pouvez exporter le modèle hello réel que vous avez utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a7722-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="a7722-108">modèle exporté du Hello inclut toutes les variables et les paramètres de hello exactement comme ils apparaissent dans le modèle d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="a7722-109">Cette approche est utile lorsque vous avez besoin d’un modèle de tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="a7722-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="a7722-110">Vous pouvez exporter un modèle qui représente l’état actuel de hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a7722-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="a7722-111">modèle exporté du Hello n’est pas basé sur un modèle que vous avez utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a7722-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="a7722-112">Au lieu de cela, il crée un modèle qui est un instantané hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a7722-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="a7722-113">modèle exporté du Hello possède de nombreuses valeurs codées en dur et probablement pas autant de paramètres que vous définissez généralement.</span><span class="sxs-lookup"><span data-stu-id="a7722-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="a7722-114">Cette approche est utile lorsque vous avez modifié le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="a7722-115">Maintenant, vous devez le groupe de ressources toocapture hello en tant que modèle.</span><span class="sxs-lookup"><span data-stu-id="a7722-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="a7722-116">Cette rubrique illustre les deux approches.</span><span class="sxs-lookup"><span data-stu-id="a7722-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="a7722-117">Déployer une solution</span><span class="sxs-lookup"><span data-stu-id="a7722-117">Deploy a solution</span></span>

<span data-ttu-id="a7722-118">tooillustrate les deux approches pour l’exportation d’un modèle, nous allons commencer en déployant un abonnement tooyour de solution.</span><span class="sxs-lookup"><span data-stu-id="a7722-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="a7722-119">Si vous avez déjà un groupe de ressources dans votre abonnement que vous souhaitez tooexport, il est inutile toodeploy cette solution.</span><span class="sxs-lookup"><span data-stu-id="a7722-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="a7722-120">Toutefois, reste hello de cet article fait référence toohello modèle pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="a7722-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="a7722-121">exemple de script Hello déploie un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a7722-121">hello example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="a7722-122">Enregistrer un modèle à partir de l’historique de déploiement</span><span class="sxs-lookup"><span data-stu-id="a7722-122">Save template from deployment history</span></span>

<span data-ttu-id="a7722-123">Vous pouvez récupérer un modèle à partir de l’historique de votre déploiement à l’aide de hello [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) commande.</span><span class="sxs-lookup"><span data-stu-id="a7722-123">You can retrieve a template from your deployment history by using hello [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="a7722-124">Hello suit exemple enregistre hello template que vous déployez précédemment :</span><span class="sxs-lookup"><span data-stu-id="a7722-124">hello following example saves hello template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="a7722-125">Il retourne emplacement hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-125">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="a7722-126">Ouvrir le fichier de hello et notez qu’il s’agit de modèle exact de hello utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a7722-126">Open hello file, and notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="a7722-127">variables et des paramètres de hello correspond à modèle hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a7722-127">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="a7722-128">Vous pouvez redéployer ce modèle.</span><span class="sxs-lookup"><span data-stu-id="a7722-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="a7722-129">Exporter un groupe de ressources en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="a7722-129">Export resource group as template</span></span>

<span data-ttu-id="a7722-130">Au lieu de récupérer un modèle à partir de l’historique de déploiement hello, vous pouvez récupérer un modèle qui représente l’état actuel de hello d’un groupe de ressources à l’aide de hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) commande.</span><span class="sxs-lookup"><span data-stu-id="a7722-130">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="a7722-131">Vous utilisez cette commande lorsque vous avez effectué le groupe de ressources de nombreuses modifications tooyour et aucun modèle existant ne représente toutes les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-131">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="a7722-132">Il retourne emplacement hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-132">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="a7722-133">Ouvrez le fichier de hello et notez qu’il est différent de celui modèle hello dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="a7722-133">Open hello file, and notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="a7722-134">Il a des paramètres différents et aucune variable.</span><span class="sxs-lookup"><span data-stu-id="a7722-134">It has different parameters and no variables.</span></span> <span data-ttu-id="a7722-135">stockage de Hello référence (SKU) et l’emplacement sont codées en dur les toovalues.</span><span class="sxs-lookup"><span data-stu-id="a7722-135">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="a7722-136">Hello suivant montre les modèles exportés hello, mais votre modèle a un nom de paramètre légèrement différentes :</span><span class="sxs-lookup"><span data-stu-id="a7722-136">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="a7722-137">Vous pouvez redéployer ce modèle, mais elle nécessite le déchiffrement d’un nom unique pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-137">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="a7722-138">nom du paramètre de Hello est légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="a7722-138">hello name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="a7722-139">Personnaliser un modèle exporté</span><span class="sxs-lookup"><span data-stu-id="a7722-139">Customize exported template</span></span>

<span data-ttu-id="a7722-140">Vous pouvez modifier cette toomake modèle il toouse plus facile et plus souple.</span><span class="sxs-lookup"><span data-stu-id="a7722-140">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="a7722-141">tooallow pour d’autres emplacements, modification hello emplacement propriété toouse hello même emplacement que le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="a7722-141">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="a7722-142">tooavoid avoir tooguess un nom uniques pour le compte de stockage, paramètre de hello remove pour le nom de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-142">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="a7722-143">Ajoutez un paramètre pour un suffixe de nom de stockage et une référence (SKU) de stockage :</span><span class="sxs-lookup"><span data-stu-id="a7722-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="a7722-144">Ajoutez une variable qui construit le nom du compte de stockage avec fonction d’uniqueString hello hello :</span><span class="sxs-lookup"><span data-stu-id="a7722-144">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="a7722-145">Définir le nom hello hello compte toohello de variable de stockage :</span><span class="sxs-lookup"><span data-stu-id="a7722-145">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="a7722-146">Affectez au paramètre de toohello hello référence (SKU) :</span><span class="sxs-lookup"><span data-stu-id="a7722-146">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="a7722-147">Votre modèle doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="a7722-147">Your template now looks like:</span></span>

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

<span data-ttu-id="a7722-148">Redéployez le modèle modifié de hello.</span><span class="sxs-lookup"><span data-stu-id="a7722-148">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7722-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a7722-149">Next steps</span></span>
* <span data-ttu-id="a7722-150">Pour plus d’informations sur l’utilisation de tooexport de portail hello un modèle, consultez [exporter un modèle Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="a7722-150">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="a7722-151">paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="a7722-151">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="a7722-152">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a7722-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
