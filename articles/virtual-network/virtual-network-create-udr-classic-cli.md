---
title: "le routage dans un classique de réseau virtuel Azure - CLI - aaaControl | Documents Microsoft"
description: "Découvrez comment toocontrol routage dans des réseaux virtuels à l’aide de hello CLI d’Azure dans le modèle de déploiement classique de hello"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>Routage de contrôle et à l’aide des équipements virtuels (classiques) utilisez hello CLI d’Azure

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interface de ligne de commande Azure](virtual-network-create-udr-arm-cli.md)
> * [Modèle](virtual-network-create-udr-arm-template.md)
> * [PowerShell (classique)](virtual-network-create-udr-classic-ps.md)
> * [Interface de ligne de commande (classique)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [contrôler le routage et d’utiliser des équipements virtuels dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-network-create-udr-arm-cli.md).

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, créer l’environnement hello [créer un réseau virtuel (classiques) à l’aide de hello CLI d’Azure](virtual-networks-create-vnet-classic-cli.md).

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Créer hello UDR pour le sous-réseau frontal de hello
table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.

1. Exécutez hello suivant le mode de commande tooswitch tooclassic :

    ```azurecli
    azure config mode asm
    ```

    Output:

        info:    New mode is asm

2. Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau frontal de hello :

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    Output:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    Paramètres :
   
   * **-l (ou --location)**. Région Azure où hello nouveau groupe de sécurité réseau doit être créé. Pour notre scénario, *westus*.
   * **-n (ou --name)**. Nom de hello nouveau groupe de sécurité réseau. Pour notre scénario, *NSG-FrontEnd*.
3. Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) :

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    Output:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    Paramètres :
   
   * **-r (ou --route-table-name)**. Nom de la table d’itinéraires hello où itinéraire de hello sera ajouté. Pour notre scénario, *UDR-FrontEnd*.
   * **-a (ou --address-prefix)**. Préfixe d’adresse de sous-réseau hello où les paquets sont destinés à. Pour notre scénario, *192.168.2.0/24*.
   * **-t (ou --next-hop-type)**. Type d'objet vers lequel le trafic sera envoyé. Les valeurs possibles sont *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.
   * **-p (ou --next-hop-ip-address**). Adresse IP de saut suivant. Pour notre scénario, *192.168.0.4*.
4. Suivante d’exécution hello commande table d’itinéraires hello tooassociate créé par hello **frontal** sous-réseau :

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Output:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    Paramètres :
   
   * **-t (ou --vnet-name)**. Nom de réseau virtuel où se trouve le sous-réseau de hello de hello. Pour notre scénario, *TestVNet*.
   * **-n (ou --subnet-name)**. Nom de table d’itinéraires hello hello sous-réseau sera ajouté à. Pour notre scénario, *FrontEnd*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Créer hello UDR pour le sous-réseau principal de hello
table d’itinéraires toocreate hello et itinéraire nécessaires pour le sous-réseau principal de hello selon le scénario hello, hello complète comme suit :

1. Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

