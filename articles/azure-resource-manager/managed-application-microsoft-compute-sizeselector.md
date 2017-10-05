---
title: "Élément d’interface utilisateur SizeSelector des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Compute.SizeSelector pour les applications gérées Azure"
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="f874d-103">Élément d’interface utilisateur Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="f874d-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="f874d-104">Contrôle permettant de sélectionner une taille pour une ou plusieurs instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f874d-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="f874d-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f874d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f874d-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="f874d-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="f874d-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="f874d-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="f874d-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="f874d-109">Remarks</span></span>
- <span data-ttu-id="f874d-110">`recommendedSizes` doit contenir au moins une taille.</span><span class="sxs-lookup"><span data-stu-id="f874d-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="f874d-111">La première taille recommandée est utilisée comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="f874d-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="f874d-112">Si une taille recommandée n’est pas disponible à l’emplacement sélectionné, la taille est automatiquement ignorée.</span><span class="sxs-lookup"><span data-stu-id="f874d-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="f874d-113">La taille recommandée suivante est alors utilisée.</span><span class="sxs-lookup"><span data-stu-id="f874d-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="f874d-114">Toute taille non spécifiée dans `constraints.allowedSizes` est masquée et toute taille non spécifiée dans `constraints.excludedSizes` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f874d-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="f874d-115">`constraints.allowedSizes`et `constraints.excludedSizes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="f874d-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="f874d-116">La liste des tailles disponibles peut être déterminée en appelant [Répertorier les tailles de machines virtuelles disponibles pour un abonnement](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="f874d-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="f874d-117">`osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.</span><span class="sxs-lookup"><span data-stu-id="f874d-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="f874d-118">Il permet de déterminer le coût du matériel des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f874d-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="f874d-119">`imageReference` est omis pour les images internes, mais est indiqué pour les images issues de tiers.</span><span class="sxs-lookup"><span data-stu-id="f874d-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="f874d-120">Il permet de déterminer le coût des logiciels des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f874d-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="f874d-121">`count` permet de définir le multiplicateur approprié pour l’élément.</span><span class="sxs-lookup"><span data-stu-id="f874d-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="f874d-122">Il prend en charge une valeur statique, telle que **2**, ou une valeur dynamique issue d’un autre élément, comme `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="f874d-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="f874d-123">La valeur par défaut est **1**.</span><span class="sxs-lookup"><span data-stu-id="f874d-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f874d-124">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="f874d-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="f874d-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f874d-125">Next steps</span></span>
* <span data-ttu-id="f874d-126">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f874d-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f874d-127">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f874d-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f874d-128">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f874d-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
