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
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="abdd0-103">Élément d’interface utilisateur Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="abdd0-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="abdd0-104">Contrôle permettant de sélectionner une taille pour une ou plusieurs instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="abdd0-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="abdd0-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="abdd0-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="abdd0-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="abdd0-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="abdd0-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="abdd0-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="abdd0-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="abdd0-109">Remarks</span></span>
- <span data-ttu-id="abdd0-110">`recommendedSizes` doit contenir au moins une taille.</span><span class="sxs-lookup"><span data-stu-id="abdd0-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="abdd0-111">Hello recommandé tout d’abord la taille est utilisée comme valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="abdd0-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="abdd0-112">Si une taille recommandée n’est pas disponible dans l’emplacement de hello sélectionné, taille de hello est automatiquement ignorée.</span><span class="sxs-lookup"><span data-stu-id="abdd0-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="abdd0-113">Au lieu de cela, hello taille recommandée suivant est utilisé.</span><span class="sxs-lookup"><span data-stu-id="abdd0-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="abdd0-114">N’importe quelle taille non spécifiée dans hello `constraints.allowedSizes` est masquée et n’importe quelle taille non spécifiée dans `constraints.excludedSizes` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="abdd0-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="abdd0-115">`constraints.allowedSizes`et `constraints.excludedSizes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="abdd0-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="abdd0-116">liste de Hello des tailles disponibles peut être déterminée en appelant [liste des tailles de machine virtuelle disponibles pour un abonnement](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="abdd0-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="abdd0-117">`osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.</span><span class="sxs-lookup"><span data-stu-id="abdd0-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="abdd0-118">Il a utilisé les coûts matériels de hello toodetermine d’ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="abdd0-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="abdd0-119">`imageReference` est omis pour les images internes, mais est indiqué pour les images issues de tiers.</span><span class="sxs-lookup"><span data-stu-id="abdd0-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="abdd0-120">Il a utilisé des coûts de machines virtuelles de hello de logiciels toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="abdd0-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="abdd0-121">`count`est tooset utilisé hello le multiplicateur approprié pour l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="abdd0-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="abdd0-122">Il prend en charge une valeur statique, telle que **2**, ou une valeur dynamique issue d’un autre élément, comme `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="abdd0-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="abdd0-123">la valeur par défaut Hello est **1**.</span><span class="sxs-lookup"><span data-stu-id="abdd0-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="abdd0-124">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="abdd0-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="abdd0-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="abdd0-125">Next steps</span></span>
* <span data-ttu-id="abdd0-126">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="abdd0-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="abdd0-127">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="abdd0-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="abdd0-128">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="abdd0-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
