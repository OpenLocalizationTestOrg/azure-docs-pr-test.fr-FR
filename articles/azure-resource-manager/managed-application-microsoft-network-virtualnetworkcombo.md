---
title: "Élément d’interface utilisateur VirtualNetworkCombo des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Network.VirtualNetworkCombo pour les applications gérées Azure"
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
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="9b546-103">Élément d’interface utilisateur Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="9b546-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="9b546-104">Groupe de contrôles pour la sélection d’un réseau virtuel nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="9b546-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="9b546-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9b546-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9b546-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="9b546-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="9b546-108">Dans la partie supérieure, l’utilisateur a sélectionné un nouveau réseau virtuel, afin que l’utilisateur puisse personnaliser le préfixe de nom et d’adresse de chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9b546-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="9b546-109">La configuration des sous-réseaux dans ce cas est facultative.</span><span class="sxs-lookup"><span data-stu-id="9b546-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="9b546-110">Dans la partie inférieure, l’utilisateur a sélectionné un nouveau réseau virtuel, afin que l’utilisateur puisse mettre en correspondance chaque sous-réseau requis par le modèle de déploiement avec un sous-réseau existant.</span><span class="sxs-lookup"><span data-stu-id="9b546-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="9b546-111">La configuration des sous-réseaux dans ce cas est requise.</span><span class="sxs-lookup"><span data-stu-id="9b546-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="9b546-112">Schéma</span><span class="sxs-lookup"><span data-stu-id="9b546-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="9b546-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="9b546-113">Remarks</span></span>
- <span data-ttu-id="9b546-114">S’il est spécifié, le premier préfixe de taille d’adresse sans chevauchement `defaultValue.addressPrefixSize` est déterminé automatiquement selon les réseaux virtuels existants de l’abonnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b546-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="9b546-115">La valeur par défaut pour `defaultValue.name` et `defaultValue.addressPrefixSize` est **null**.</span><span class="sxs-lookup"><span data-stu-id="9b546-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="9b546-116">`constraints.minAddressPrefixSize` doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="9b546-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="9b546-117">Des réseaux virtuels existants dont l’espace d’adressage est plus petit que la valeur spécifiée ne sont pas disponibles à la sélection.</span><span class="sxs-lookup"><span data-stu-id="9b546-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="9b546-118">`subnets` doit être spécifié, et `constraints.minAddressPrefixSize` doit être spécifié pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9b546-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="9b546-119">Lorsque vous créez un réseau virtuel, le préfixe d’adresse de chaque sous-réseau est calculé automatiquement en fonction du préfixe d’adresse du réseau virtuel et du `addressPrefixSize` respectif.</span><span class="sxs-lookup"><span data-stu-id="9b546-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="9b546-120">Lorsque vous utilisez un réseau virtuel existant, tous les sous-réseaux dont la taille est inférieure à la valeur `constraints.minAddressPrefixSize` respective ne sont pas disponibles à la sélection.</span><span class="sxs-lookup"><span data-stu-id="9b546-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="9b546-121">En outre, si cet élément est spécifié, les sous-réseaux qui ne contiennent pas au moins `minAddressCount` adresses disponibles ne sont pas disponibles à la sélection.</span><span class="sxs-lookup"><span data-stu-id="9b546-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="9b546-122">La valeur par défaut est **0**.</span><span class="sxs-lookup"><span data-stu-id="9b546-122">The default value is **0**.</span></span> <span data-ttu-id="9b546-123">Pour vous assurer que les adresses disponibles sont contiguës, spécifiez **true** pour `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="9b546-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="9b546-124">La valeur par défaut est **true**.</span><span class="sxs-lookup"><span data-stu-id="9b546-124">The default value is **true**.</span></span>
- <span data-ttu-id="9b546-125">La création de sous-réseaux dans un réseau virtuel n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="9b546-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="9b546-126">Si `options.hideExisting` est défini sur **true**, l’utilisateur ne peut pas choisir de réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="9b546-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="9b546-127">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="9b546-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9b546-128">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="9b546-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="9b546-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b546-129">Next steps</span></span>
* <span data-ttu-id="9b546-130">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b546-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9b546-131">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b546-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9b546-132">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="9b546-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>