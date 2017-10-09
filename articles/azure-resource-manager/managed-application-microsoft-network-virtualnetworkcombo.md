---
title: "élément de l’interface utilisateur de VirtualNetworkCombo pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Network.VirtualNetworkCombo pour des Applications managées Azure"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="3a738-103">Élément d’interface utilisateur Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="3a738-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="3a738-104">Groupe de contrôles pour la sélection d’un réseau virtuel nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="3a738-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="3a738-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3a738-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="3a738-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="3a738-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="3a738-108">En mode filaire supérieur de hello, utilisateur de hello a choisi un nouveau réseau virtuel, afin de l’utilisateur de hello peut personnaliser le préfixe de nom et l’adresse de chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="3a738-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="3a738-109">La configuration des sous-réseaux dans ce cas est facultative.</span><span class="sxs-lookup"><span data-stu-id="3a738-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="3a738-110">Hello bas filaire, utilisateur de hello a choisi un réseau virtuel existant, afin de l’utilisateur de hello doit mapper chaque modèle de déploiement de sous-réseau hello nécessite tooan des sous-réseau existant.</span><span class="sxs-lookup"><span data-stu-id="3a738-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="3a738-111">La configuration des sous-réseaux dans ce cas est requise.</span><span class="sxs-lookup"><span data-stu-id="3a738-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="3a738-112">Schéma</span><span class="sxs-lookup"><span data-stu-id="3a738-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="3a738-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="3a738-113">Remarks</span></span>
- <span data-ttu-id="3a738-114">Si spécifié, hello premier préfixe d’adresse sans chevauchement de taille `defaultValue.addressPrefixSize` est déterminée automatiquement en fonction des réseaux virtuels existants dans l’abonnement de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="3a738-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="3a738-115">Hello la valeur par défaut de `defaultValue.name` et `defaultValue.addressPrefixSize` est **null**.</span><span class="sxs-lookup"><span data-stu-id="3a738-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="3a738-116">`constraints.minAddressPrefixSize` doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="3a738-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="3a738-117">Des réseaux virtuels existants avec un espace d’adressage plus petit que hello valeur spécifiée ne sont pas disponibles pour la sélection.</span><span class="sxs-lookup"><span data-stu-id="3a738-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="3a738-118">`subnets` doit être spécifié, et `constraints.minAddressPrefixSize` doit être spécifié pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="3a738-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="3a738-119">Lorsque vous créez un réseau virtuel, préfixe d’adresse de chaque sous-réseau est calculée automatiquement en fonction de préfixe d’adresse du réseau virtuel hello et respectifs `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="3a738-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="3a738-120">Lorsque vous utilisez un réseau virtuel existant, tous les sous-réseaux dont la taille est inférieure à la valeur `constraints.minAddressPrefixSize` respective ne sont pas disponibles à la sélection.</span><span class="sxs-lookup"><span data-stu-id="3a738-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="3a738-121">En outre, si cet élément est spécifié, les sous-réseaux qui ne contiennent pas au moins `minAddressCount` adresses disponibles ne sont pas disponibles à la sélection.</span><span class="sxs-lookup"><span data-stu-id="3a738-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="3a738-122">la valeur par défaut Hello est **0**.</span><span class="sxs-lookup"><span data-stu-id="3a738-122">hello default value is **0**.</span></span> <span data-ttu-id="3a738-123">tooensure qui hello adresses disponibles sont contiguës, spécifiez **true** pour `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="3a738-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="3a738-124">la valeur par défaut Hello est **true**.</span><span class="sxs-lookup"><span data-stu-id="3a738-124">hello default value is **true**.</span></span>
- <span data-ttu-id="3a738-125">La création de sous-réseaux dans un réseau virtuel n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="3a738-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="3a738-126">Si `options.hideExisting` est **true**, utilisateur de hello ne pouvez pas choisir un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="3a738-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="3a738-127">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="3a738-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="3a738-128">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="3a738-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="3a738-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a738-129">Next steps</span></span>
* <span data-ttu-id="3a738-130">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a738-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3a738-131">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a738-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="3a738-132">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="3a738-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
