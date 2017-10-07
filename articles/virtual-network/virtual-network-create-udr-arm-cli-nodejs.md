---
title: "aaaControl équipements virtuels et de routage à l’aide de hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocontrol équipements virtuels et de routage à l’aide de hello Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a>Créer des itinéraires définis par l’utilisateur (UDR) à l’aide de hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interface de ligne de commande Azure](virtual-network-create-udr-arm-cli.md)
> * [Modèle](virtual-network-create-udr-arm-template.md)
> * [PowerShell (classique)](virtual-network-create-udr-classic-ps.md)
> * [Interface de ligne de commande (classique)](virtual-network-create-udr-classic-cli.md)

Créer un routage personnalisé et des équipements virtuels à l’aide de hello CLI d’Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete 

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes : 

- [Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer des environnement de test hello en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello Si nécessaire et suivez les instructions hello dans hello portal.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Créer hello UDR pour le sous-réseau frontal de hello
table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.

1. Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau frontal de hello :

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    Output:
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    Paramètres :
   
   * **-g (ou --resource-group)**. Nom du groupe de ressources hello où hello UDR sera créé. Pour notre scénario, *TestRG*.
   * **-l (ou --location)**. Région Azure où hello UDR nouvelle sera créée. Pour notre scénario, *westus*.
   * **-n (ou --name)**. Nom de hello UDR de nouveau. Pour notre scénario, *UDR-FrontEnd*.
2. Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) :

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    Output:
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    Paramètres :
   
   * **-r (ou --route-table-name)**. Nom de la table d’itinéraires hello où itinéraire de hello sera ajouté. Pour notre scénario, *UDR-FrontEnd*.
   * **-a (ou --address-prefix)**. Préfixe d’adresse de sous-réseau hello où les paquets sont destinés à. Pour notre scénario, *192.168.2.0/24*.
   * **-y (ou --next-hop-type)**. Type d'objet vers lequel le trafic sera envoyé. Les valeurs possibles sont *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.
   * **-p (ou --next-hop-ip-address**). Adresse IP de saut suivant. Pour notre scénario, *192.168.0.4*.
3. Table d’itinéraires hello tooassociate créé ci-dessus hello de commandes suivante d’exécution hello **frontal** sous-réseau :

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Output:
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    Paramètres :
   
   * **-e (ou --vnet-name)**. Nom de réseau virtuel où se trouve le sous-réseau de hello de hello. Pour notre scénario, *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Créer hello UDR pour le sous-réseau principal de hello
toocreate hello table d’itinéraires et Router nécessaires pour le sous-réseau principal de hello selon le scénario hello ci-dessus, hello complète comme suit :

1. Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Activer le transfert IP sur FW1
le transfert IP tooenable Bonjour carte réseau utilisée par **FW1**complète hello comme suit :

1. Exécutez la commande hello qui suit et notez la valeur hello pour **transfert activer une IP**. Il doit être défini trop*false*.

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    Output:
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. Exécutez hello après le transfert IP commande tooenable :

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    Output:
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    Paramètres :
   
   * **-f (ou --enable-ip-forwarding)**. *true* ou *false*.

