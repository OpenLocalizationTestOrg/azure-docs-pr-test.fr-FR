---
title: "le routage dans un classique de réseau virtuel Azure - PowerShell - aaaControl | Documents Microsoft"
description: "Découvrez comment toocontrol routage dans des réseaux virtuels à l’aide de PowerShell | Classique"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>Contrôle du routage et utilisation des appliances virtuelles (classiques) à l'aide de PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interface de ligne de commande Azure](virtual-network-create-udr-arm-cli.md)
> * [Modèle](virtual-network-create-udr-arm-template.md)
> * [PowerShell (classique)](virtual-network-create-udr-classic-ps.md)
> * [Interface de ligne de commande (classique)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique. Veillez à bien comprendre les [modèles et outils de déploiement](../azure-resource-manager/resource-manager-deployment-model.md) avant d’utiliser une ressource Azure. Vous pouvez afficher la documentation hello pour différents outils en sélectionnant une option haut hello de cet article. Cet article décrit le modèle de déploiement classique hello.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

l’exemple Hello Azure PowerShell commandes ci-dessous attendent un simple environnement déjà créé en fonction de scénario hello ci-dessus. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, créer l’environnement hello [créer un réseau virtuel (classiques) à l’aide de PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Créer hello UDR pour le sous-réseau frontal de hello
table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.

1. Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau frontal de hello :

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) :

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **frontal** sous-réseau :

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Créer hello UDR pour le sous-réseau principal de hello
table d’itinéraires toocreate hello et d’itinéraire si nécessaire pour la sauvegarde de hello fin sous-réseau selon le scénario de hello, terminer hello comme suit :

1. Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>Activer le transfert IP sur hello FW1 VM

transfert IP tooenable Bonjour FW1 VM, hello complète comme suit :

1. Exécutez hello suivant l’état du transfert IP hello de toocheck la commande :

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. Suivante d’exécution hello commande tooenable le transfert IP pour hello *FW1* machine virtuelle :

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
