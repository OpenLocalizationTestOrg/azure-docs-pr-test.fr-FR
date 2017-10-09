---
title: "élément de l’interface utilisateur de SizeSelector pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Compute.SizeSelector pour des Applications managées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Élément d’interface utilisateur Microsoft.Compute.SizeSelector
Contrôle permettant de sélectionner une taille pour une ou plusieurs instances de machine virtuelle. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>Schéma
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Remarques
- `recommendedSizes` doit contenir au moins une taille. Hello recommandé tout d’abord la taille est utilisée comme valeur par défaut hello.
- Si une taille recommandée n’est pas disponible dans l’emplacement de hello sélectionné, taille de hello est automatiquement ignorée. Au lieu de cela, hello taille recommandée suivant est utilisé.
- N’importe quelle taille non spécifiée dans hello `constraints.allowedSizes` est masquée et n’importe quelle taille non spécifiée dans `constraints.excludedSizes` s’affiche.
`constraints.allowedSizes`et `constraints.excludedSizes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément. liste de Hello des tailles disponibles peut être déterminée en appelant [liste des tailles de machine virtuelle disponibles pour un abonnement](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- `osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**. Il a utilisé les coûts matériels de hello toodetermine d’ordinateurs virtuels hello.
- `imageReference` est omis pour les images internes, mais est indiqué pour les images issues de tiers. Il a utilisé des coûts de machines virtuelles de hello de logiciels toodetermine hello.
- `count`est tooset utilisé hello le multiplicateur approprié pour l’élément de hello. Il prend en charge une valeur statique, telle que **2**, ou une valeur dynamique issue d’un autre élément, comme `[steps('step1').vmCount]`. la valeur par défaut Hello est **1**.

## <a name="sample-output"></a>Exemple de sortie
```json
"Standard_D1"
```

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
