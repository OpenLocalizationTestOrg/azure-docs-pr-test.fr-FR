---
title: "aaaControl équipements virtuels et de routage à l’aide de hello Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocontrol équipements virtuels et de routage à l’aide de hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Créer des itinéraires définis par l’utilisateur (UDR) à l’aide de hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interface de ligne de commande Azure](virtual-network-create-udr-arm-cli.md)
> * [Modèle](virtual-network-create-udr-arm-template.md)
> * [PowerShell (déploiement Classic)](virtual-network-create-udr-classic-ps.md)
> * [CLI (déploiement Classic)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete 

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes : 

- [Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello 
- [Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer des environnement de test hello en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello Si nécessaire et suivez les instructions hello dans hello portal.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Créer hello UDR pour le sous-réseau frontal de hello
table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.

1. Créer une table d’itinéraires pour le sous-réseau frontal de hello avec hello [créer de table de routage de réseau az](/cli/azure/network/route-table#create) commande :

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Output:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Créez un itinéraire qui envoie tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) à l’aide de hello [itinéraire de table d’itinéraires réseau az créer](/cli/azure/network/route-table/route#create) commande :

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Output:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Paramètres :

    * **--route-table-name**. Nom de la table d’itinéraires hello où itinéraire de hello sera ajouté. Pour notre scénario, *UDR-FrontEnd*.
    * **--address-prefix**. Préfixe d’adresse de sous-réseau hello où les paquets sont destinés à. Pour notre scénario, *192.168.2.0/24*.
    * **--next-hop-type**. Type d'objet vers lequel le trafic sera envoyé. Les valeurs possibles sont *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.
    * **--next-hop-ip-address**. Adresse IP de saut suivant. Pour notre scénario, *192.168.0.4*.

3. Exécutez hello [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update) table d’itinéraires commande tooassociate hello créé ci-dessus hello **frontal** sous-réseau :

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Output:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Paramètres :
    
    * **--vnet-name**. Nom de réseau virtuel où se trouve le sous-réseau de hello de hello. Pour notre scénario, *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Créer hello UDR pour le sous-réseau principal de hello

toocreate hello table d’itinéraires et Router nécessaires pour le sous-réseau principal de hello selon le scénario hello ci-dessus, hello complète comme suit :

1. Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Activer le transfert IP sur FW1

le transfert IP tooenable Bonjour carte réseau utilisée par **FW1**complète hello comme suit :

1. Exécutez hello [az réseau nic afficher](/cli/azure/network/nic#show) avec un Bonjour de toodisplay JMESPATH filtre actuel **-ip-activer le transfert** valeur **transfert activer une IP**. Il doit être défini trop*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Output:

        false

2. Exécutez hello après le transfert IP commande tooenable :

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    Vous pouvez examiner la console de toohello en flux continu de sortie hello ou simplement retester pour hello spécifique **enableIpForwarding** valeur :

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Output:

        true

    Paramètres :

    **--ip-forwarding** : *true* ou *false*.

