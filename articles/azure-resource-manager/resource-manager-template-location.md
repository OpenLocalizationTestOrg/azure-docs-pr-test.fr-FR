---
title: "Emplacement des ressources Azure dans un modèle | Microsoft Docs"
description: "Explique comment définir un emplacement pour une ressource dans un modèle Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="80b67-103">Définir l’emplacement des ressources dans des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="80b67-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="80b67-104">Lorsque vous déployez un modèle, vous devez fournir un emplacement pour chaque ressource.</span><span class="sxs-lookup"><span data-stu-id="80b67-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="80b67-105">Cette rubrique vous explique comment déterminer quels emplacements sont disponibles pour votre abonnement pour chaque type de ressource.</span><span class="sxs-lookup"><span data-stu-id="80b67-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="80b67-106">Déterminer les emplacements pris en charge</span><span class="sxs-lookup"><span data-stu-id="80b67-106">Determine supported locations</span></span>

<span data-ttu-id="80b67-107">Pour obtenir une liste complète des emplacements pris en charge pour chaque type de ressource, consultez [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="80b67-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="80b67-108">Toutefois, votre abonnement peut ne pas avoir accès à tous les emplacements de cette liste.</span><span class="sxs-lookup"><span data-stu-id="80b67-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="80b67-109">Pour afficher une liste personnalisée des emplacements disponibles pour votre abonnement, utilisez Azure PowerShell ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="80b67-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="80b67-110">L’exemple suivant utilise PowerShell pour obtenir les emplacements pour le type de ressource `Microsoft.Web\sites` :</span><span class="sxs-lookup"><span data-stu-id="80b67-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="80b67-111">L’exemple suivant utilise Azure CLI 2.0 pour obtenir les emplacements pour le type de ressource `Microsoft.Web\sites` :</span><span class="sxs-lookup"><span data-stu-id="80b67-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="80b67-112">Définir les emplacements dans un modèle</span><span class="sxs-lookup"><span data-stu-id="80b67-112">Set location in template</span></span>

<span data-ttu-id="80b67-113">Après avoir déterminé les emplacements pris en charge pour vos ressources, vous devez définir cet emplacement dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="80b67-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="80b67-114">Le moyen le plus simple pour définir cette valeur consiste à créer un groupe de ressources dans un emplacement qui prend en charge les types de ressources, puis de définir chaque emplacement sur `[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="80b67-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="80b67-115">Vous pouvez redéployer le modèle dans des groupes de ressources à des emplacements différents et ne pas modifier les valeurs dans le modèle ou les paramètres.</span><span class="sxs-lookup"><span data-stu-id="80b67-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="80b67-116">L’exemple suivant illustre le déploiement d’un compte de stockage au même emplacement que le groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="80b67-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="80b67-117">Si vous devez coder en dur l’emplacement dans votre modèle, indiquez le nom de l’une des régions prises en charge.</span><span class="sxs-lookup"><span data-stu-id="80b67-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="80b67-118">L’exemple suivant montre un compte de stockage qui est toujours déployé dans la région Nord du centre des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="80b67-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="80b67-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80b67-119">Next steps</span></span>
* <span data-ttu-id="80b67-120">Pour des recommandations sur la création de modèles, consultez [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="80b67-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

