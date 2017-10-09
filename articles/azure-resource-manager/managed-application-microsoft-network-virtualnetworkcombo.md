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
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Élément d’interface utilisateur Microsoft.Network.VirtualNetworkCombo
Groupe de contrôles pour la sélection d’un réseau virtuel nouveau ou existant. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- En mode filaire supérieur de hello, utilisateur de hello a choisi un nouveau réseau virtuel, afin de l’utilisateur de hello peut personnaliser le préfixe de nom et l’adresse de chaque sous-réseau. La configuration des sous-réseaux dans ce cas est facultative.
- Hello bas filaire, utilisateur de hello a choisi un réseau virtuel existant, afin de l’utilisateur de hello doit mapper chaque modèle de déploiement de sous-réseau hello nécessite tooan des sous-réseau existant. La configuration des sous-réseaux dans ce cas est requise.

## <a name="schema"></a>Schéma
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

## <a name="remarks"></a>Remarques
- Si spécifié, hello premier préfixe d’adresse sans chevauchement de taille `defaultValue.addressPrefixSize` est déterminée automatiquement en fonction des réseaux virtuels existants dans l’abonnement de l’utilisateur hello.
- Hello la valeur par défaut de `defaultValue.name` et `defaultValue.addressPrefixSize` est **null**.
- `constraints.minAddressPrefixSize` doit être spécifié. Des réseaux virtuels existants avec un espace d’adressage plus petit que hello valeur spécifiée ne sont pas disponibles pour la sélection.
- `subnets` doit être spécifié, et `constraints.minAddressPrefixSize` doit être spécifié pour chaque sous-réseau.
- Lorsque vous créez un réseau virtuel, préfixe d’adresse de chaque sous-réseau est calculée automatiquement en fonction de préfixe d’adresse du réseau virtuel hello et respectifs `addressPrefixSize`.
- Lorsque vous utilisez un réseau virtuel existant, tous les sous-réseaux dont la taille est inférieure à la valeur `constraints.minAddressPrefixSize` respective ne sont pas disponibles à la sélection. En outre, si cet élément est spécifié, les sous-réseaux qui ne contiennent pas au moins `minAddressCount` adresses disponibles ne sont pas disponibles à la sélection.
la valeur par défaut Hello est **0**. tooensure qui hello adresses disponibles sont contiguës, spécifiez **true** pour `requireContiguousAddresses`. la valeur par défaut Hello est **true**.
- La création de sous-réseaux dans un réseau virtuel n’est pas prise en charge.
- Si `options.hideExisting` est **true**, utilisateur de hello ne pouvez pas choisir un réseau virtuel existant. la valeur par défaut Hello est **false**.

## <a name="sample-output"></a>Exemple de sortie
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

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
