---
title: "emplacement dans le modèle de la ressource aaaAzure | Documents Microsoft"
description: "Montre comment tooset un emplacement pour une ressource dans un modèle Azure Resource Manager"
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
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="cb494-103">Définir l’emplacement des ressources dans des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cb494-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="cb494-104">Lorsque vous déployez un modèle, vous devez fournir un emplacement pour chaque ressource.</span><span class="sxs-lookup"><span data-stu-id="cb494-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="cb494-105">Cette rubrique montre comment les emplacements hello toodetermine abonnement tooyour disponibles pour chaque ressource de type.</span><span class="sxs-lookup"><span data-stu-id="cb494-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="cb494-106">Déterminer les emplacements pris en charge</span><span class="sxs-lookup"><span data-stu-id="cb494-106">Determine supported locations</span></span>

<span data-ttu-id="cb494-107">Pour obtenir une liste complète des emplacements pris en charge pour chaque type de ressource, consultez [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="cb494-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="cb494-108">Toutefois, votre abonnement peut-être pas accès tooall hello emplacements dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="cb494-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="cb494-109">toosee une liste personnalisée des emplacements qui sont disponibles tooyour abonnement, utilisez Azure PowerShell ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="cb494-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="cb494-110">Hello exemple suivant utilise PowerShell tooget hello emplacements pour hello `Microsoft.Web\sites` type de ressource :</span><span class="sxs-lookup"><span data-stu-id="cb494-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="cb494-111">Hello exemple suivant utilise Azure CLI 2.0 tooget hello emplacements pour hello `Microsoft.Web\sites` type de ressource :</span><span class="sxs-lookup"><span data-stu-id="cb494-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="cb494-112">Définir les emplacements dans un modèle</span><span class="sxs-lookup"><span data-stu-id="cb494-112">Set location in template</span></span>

<span data-ttu-id="cb494-113">Après avoir déterminé les emplacements hello pris en charge pour vos ressources, vous devez tooset cet emplacement dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="cb494-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="cb494-114">Hello tooset de façon plus simple cette valeur est toocreate une ressource de groupe dans un emplacement qui prend en charge les types de ressources hello et définir chaque emplacement trop`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="cb494-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="cb494-115">Vous pouvez redéployer les groupes de tooresource modèle hello dans différents emplacements et modifie pas les valeurs dans le modèle de hello ou des paramètres.</span><span class="sxs-lookup"><span data-stu-id="cb494-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="cb494-116">Hello suivant montre un compte de stockage qui est déployé toohello même emplacement que le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="cb494-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

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

<span data-ttu-id="cb494-117">Si vous avez besoin d’emplacement de hello toohardcode dans votre modèle, fournir hello nom de l’une des régions de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="cb494-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="cb494-118">Bonjour à l’exemple suivant montre un compte de stockage est toujours déployé tooNorth du centre des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="cb494-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cb494-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cb494-119">Next steps</span></span>
* <span data-ttu-id="cb494-120">Pour obtenir des recommandations sur la façon toocreate modèles, consultez [meilleures pratiques pour la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="cb494-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

