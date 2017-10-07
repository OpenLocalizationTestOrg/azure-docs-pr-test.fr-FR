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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Définir l’emplacement des ressources dans des modèles Azure Resource Manager
Lorsque vous déployez un modèle, vous devez fournir un emplacement pour chaque ressource. Cette rubrique montre comment les emplacements hello toodetermine abonnement tooyour disponibles pour chaque ressource de type.

## <a name="determine-supported-locations"></a>Déterminer les emplacements pris en charge

Pour obtenir une liste complète des emplacements pris en charge pour chaque type de ressource, consultez [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/). Toutefois, votre abonnement peut-être pas accès tooall hello emplacements dans cette liste. toosee une liste personnalisée des emplacements qui sont disponibles tooyour abonnement, utilisez Azure PowerShell ou CLI d’Azure. 

Hello exemple suivant utilise PowerShell tooget hello emplacements pour hello `Microsoft.Web\sites` type de ressource :

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Hello exemple suivant utilise Azure CLI 2.0 tooget hello emplacements pour hello `Microsoft.Web\sites` type de ressource :

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Définir les emplacements dans un modèle

Après avoir déterminé les emplacements hello pris en charge pour vos ressources, vous devez tooset cet emplacement dans votre modèle. Hello tooset de façon plus simple cette valeur est toocreate une ressource de groupe dans un emplacement qui prend en charge les types de ressources hello et définir chaque emplacement trop`[resourceGroup().location]`. Vous pouvez redéployer les groupes de tooresource modèle hello dans différents emplacements et modifie pas les valeurs dans le modèle de hello ou des paramètres. 

Hello suivant montre un compte de stockage qui est déployé toohello même emplacement que le groupe de ressources hello :

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

Si vous avez besoin d’emplacement de hello toohardcode dans votre modèle, fournir hello nom de l’une des régions de hello pris en charge. Bonjour à l’exemple suivant montre un compte de stockage est toujours déployé tooNorth du centre des États-Unis :

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

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des recommandations sur la façon toocreate modèles, consultez [meilleures pratiques pour la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).

