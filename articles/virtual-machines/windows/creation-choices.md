---
title: "aaaDifferent manières toocreate un ordinateur virtuel Windows Azure | Documents Microsoft"
description: "Répertorie les différentes façons de hello toocreate machine virtuelle Windows avec le Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Différentes façons toocreate une machine virtuelle Windows

Azure offre toocreate de différentes façons d’un ordinateur virtuel, car les machines virtuelles sont adaptés à différents utilisateurs et à des fins. Cela signifie que vous devez toomake certains choix sur l’ordinateur virtuel de hello et comment toocreate il. Cet article vous fournit un résumé de ces choix et des liens tooinstructions.

## <a name="azure-portal"></a>Portail Azure
À l’aide de hello portail Azure d’est une tootry facilement à une machine virtuelle, en particulier si vous démarrez avec Azure. 

[Créer une machine virtuelle exécutant Windows à l’aide du portail de hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Modèle
Les machines virtuelles requièrent une combinaison de ressources (par exemple un groupe à haute disponibilité et des comptes de stockage). Plutôt que le déploiement et la gestion de chaque ressource séparément, vous pouvez créer un modèle Azure Resource Manager qui déploie et configure toutes les ressources hello dans une opération unique et coordonnée.

* [Création d’une machine virtuelle Windows avec un modèle du Gestionnaire de ressources](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Si vous préférez travailler dans une invite de commandes, vous pouvez utiliser Azure PowerShell.

* [Créer une machine virtuelle Windows à l’aide de PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Utilisez Visual Studio toobuild, gérer et déployer des machines virtuelles avec hello Windows Azure Tools pour Visual Studio et hello Azure SDK.

[Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

