---
title: "modèle de gestionnaire de ressources aaaExport avec CLI d’Azure | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et Azure CLI tooexport un modèle à partir d’un groupe de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="f6139-103">Exporter des modèles Azure Resource Manager avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f6139-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="f6139-104">Le Gestionnaire de ressources vous permet de tooexport un modèle de gestionnaire de ressources à partir de ressources existants dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f6139-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="f6139-105">Vous pouvez utiliser ce toolearn modèle généré sur hello modèle syntaxe ou tooautomate hello redéploiement de votre solution en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="f6139-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="f6139-106">Il est important toonote qu’il existe deux façons différentes tooexport un modèle :</span><span class="sxs-lookup"><span data-stu-id="f6139-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="f6139-107">Vous pouvez exporter le modèle hello réel que vous avez utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6139-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="f6139-108">modèle exporté du Hello inclut toutes les variables et les paramètres de hello exactement comme ils apparaissent dans le modèle d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="f6139-109">Cette approche est utile lorsque vous avez besoin d’un modèle de tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="f6139-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="f6139-110">Vous pouvez exporter un modèle qui représente l’état actuel de hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f6139-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="f6139-111">modèle exporté du Hello n’est pas basé sur un modèle que vous avez utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6139-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="f6139-112">Au lieu de cela, il crée un modèle qui est un instantané hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f6139-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="f6139-113">modèle exporté du Hello possède de nombreuses valeurs codées en dur et probablement pas autant de paramètres que vous définissez généralement.</span><span class="sxs-lookup"><span data-stu-id="f6139-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="f6139-114">Cette approche est utile lorsque vous avez modifié le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="f6139-115">Maintenant, vous devez le groupe de ressources toocapture hello en tant que modèle.</span><span class="sxs-lookup"><span data-stu-id="f6139-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="f6139-116">Cette rubrique illustre les deux approches.</span><span class="sxs-lookup"><span data-stu-id="f6139-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="f6139-117">Déployer une solution</span><span class="sxs-lookup"><span data-stu-id="f6139-117">Deploy a solution</span></span>

<span data-ttu-id="f6139-118">tooillustrate les deux approches pour l’exportation d’un modèle, nous allons commencer en déployant un abonnement tooyour de solution.</span><span class="sxs-lookup"><span data-stu-id="f6139-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="f6139-119">Si vous avez déjà un groupe de ressources dans votre abonnement que vous souhaitez tooexport, il est inutile toodeploy cette solution.</span><span class="sxs-lookup"><span data-stu-id="f6139-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="f6139-120">Toutefois, reste hello de cet article fait référence toohello modèle pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="f6139-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="f6139-121">exemple de script Hello déploie un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f6139-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="f6139-122">Enregistrer un modèle à partir de l’historique de déploiement</span><span class="sxs-lookup"><span data-stu-id="f6139-122">Save template from deployment history</span></span>

<span data-ttu-id="f6139-123">Vous pouvez récupérer un modèle à partir de l’historique de votre déploiement à l’aide de hello [exportation de déploiement de groupe az](/cli/azure/group/deployment#export) commande.</span><span class="sxs-lookup"><span data-stu-id="f6139-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="f6139-124">Hello suit exemple enregistre hello template que vous déployez précédemment :</span><span class="sxs-lookup"><span data-stu-id="f6139-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="f6139-125">Il retourne le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-125">It returns hello template.</span></span> <span data-ttu-id="f6139-126">Copier hello JSON et les enregistrer en tant que fichier.</span><span class="sxs-lookup"><span data-stu-id="f6139-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="f6139-127">Notez qu’il s’agit de modèle exact de hello utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6139-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="f6139-128">variables et des paramètres de hello correspond à modèle hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="f6139-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="f6139-129">Vous pouvez redéployer ce modèle.</span><span class="sxs-lookup"><span data-stu-id="f6139-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="f6139-130">Exporter un groupe de ressources en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="f6139-130">Export resource group as template</span></span>

<span data-ttu-id="f6139-131">Au lieu de récupérer un modèle à partir de l’historique de déploiement hello, vous pouvez récupérer un modèle qui représente l’état actuel de hello d’un groupe de ressources à l’aide de hello [exportation de groupe az](/cli/azure/group#export) commande.</span><span class="sxs-lookup"><span data-stu-id="f6139-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="f6139-132">Vous utilisez cette commande lorsque vous avez effectué le groupe de ressources de nombreuses modifications tooyour et aucun modèle existant ne représente toutes les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="f6139-133">Il retourne le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-133">It returns hello template.</span></span> <span data-ttu-id="f6139-134">Copier hello JSON et les enregistrer en tant que fichier.</span><span class="sxs-lookup"><span data-stu-id="f6139-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="f6139-135">Notez qu’il est différent de celui modèle hello dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="f6139-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="f6139-136">Il a des paramètres différents et aucune variable.</span><span class="sxs-lookup"><span data-stu-id="f6139-136">It has different parameters and no variables.</span></span> <span data-ttu-id="f6139-137">stockage de Hello référence (SKU) et l’emplacement sont codées en dur les toovalues.</span><span class="sxs-lookup"><span data-stu-id="f6139-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="f6139-138">Hello suivant montre les modèles exportés hello, mais votre modèle a un nom de paramètre légèrement différentes :</span><span class="sxs-lookup"><span data-stu-id="f6139-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="f6139-139">Vous pouvez redéployer ce modèle, mais elle nécessite le déchiffrement d’un nom unique pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="f6139-140">nom du paramètre de Hello est légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="f6139-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="f6139-141">Personnaliser un modèle exporté</span><span class="sxs-lookup"><span data-stu-id="f6139-141">Customize exported template</span></span>

<span data-ttu-id="f6139-142">Vous pouvez modifier cette toomake modèle il toouse plus facile et plus souple.</span><span class="sxs-lookup"><span data-stu-id="f6139-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="f6139-143">tooallow pour d’autres emplacements, modification hello emplacement propriété toouse hello même emplacement que le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="f6139-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="f6139-144">tooavoid avoir tooguess un nom uniques pour le compte de stockage, paramètre de hello remove pour le nom de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="f6139-145">Ajoutez un paramètre pour un suffixe de nom de stockage et une référence (SKU) de stockage :</span><span class="sxs-lookup"><span data-stu-id="f6139-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="f6139-146">Ajoutez une variable qui construit le nom du compte de stockage avec fonction d’uniqueString hello hello :</span><span class="sxs-lookup"><span data-stu-id="f6139-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="f6139-147">Définir le nom hello hello compte toohello de variable de stockage :</span><span class="sxs-lookup"><span data-stu-id="f6139-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="f6139-148">Affectez au paramètre de toohello hello référence (SKU) :</span><span class="sxs-lookup"><span data-stu-id="f6139-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="f6139-149">Votre modèle doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="f6139-149">Your template now looks like:</span></span>

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

<span data-ttu-id="f6139-150">Redéployez le modèle modifié de hello.</span><span class="sxs-lookup"><span data-stu-id="f6139-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6139-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6139-151">Next steps</span></span>
* <span data-ttu-id="f6139-152">Pour plus d’informations sur l’utilisation de tooexport de portail hello un modèle, consultez [exporter un modèle Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="f6139-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="f6139-153">paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="f6139-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="f6139-154">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="f6139-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>