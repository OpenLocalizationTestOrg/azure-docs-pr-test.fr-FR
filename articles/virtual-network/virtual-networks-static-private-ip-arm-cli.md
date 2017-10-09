---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les ordinateurs virtuels à l’aide de hello Azure interface de ligne de commande (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Configurer des adresses IP privées pour un ordinateur virtuel à l’aide de hello Azure CLI 2.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete 

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes : 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique hello](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> Hello exemples Azure CLI 2.0 de commandes ci-dessous s’attendre à un environnement simple déjà créé. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Spécifier une adresse IP privée statique lors de la création d’une machine virtuelle

toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet* avec une adresse IP privée statique de *192.168.1.101*, Suivez les étapes de hello ci-dessous :

1. Si vous n’avez pas encore, installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). 

2. Créer une adresse IP publique pour hello VM par hello [az réseau public-ip créer](/cli/azure/network/public-ip#create) commande. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.

    > [!NOTE]
    > Vous voulez ou devez toouse des valeurs différentes pour que les arguments de cette et les étapes suivantes, en fonction de votre environnement.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Sortie attendue :
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Nom du groupe de ressources hello dans le toocreate hello adresse IP publique.
   * `--name`: Nom de l’adresse IP publique hello.
   * `--location`: Région azure qui toocreate hello adresse IP publique.

3. Exécutez hello [créer des cartes réseau du réseau az](/cli/azure/network/nic#create) commande toocreate une carte réseau avec une adresse IP statique privée. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Sortie attendue :
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Paramètres :

    * `--private-ip-address`: Statique adresse IP privée pour hello carte réseau.
    * `--vnet-name`: Nom de réseau virtuel de hello dans le toocreate hello carte réseau.
    * `--subnet`: Nom de sous-réseau hello dans le hello toocreate carte réseau.

4. Exécutez hello [créer de machine virtuelle azure](/cli/azure/vm/nic#create) commande toocreate hello machine virtuelle en utilisant l’adresse IP publique hello et la carte réseau créé précédemment. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Sortie attendue :
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Paramètres de base de hello [az vm créer](/cli/azure/vm#create) paramètres.

   * `--nics`: Nom Hello de toowhich hello carte réseau virtuelle est attachée.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Récupérer des informations d’adresse IP privée statique pour une machine virtuelle

tooview hello adresse IP privée statique que vous avez créé, exécutez hello suivant commande CLI d’Azure et observer les valeurs hello pour *IP privée de la méthode d’allocation* et *adresse IP privée*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Sortie attendue :

```json
"192.168.1.101"
```

toodisplay hello plus précisément les informations IP spécifiques de hello carte réseau pour cette machine virtuelle, hello de requête carte réseau :

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

sortie de Hello est quelque chose comme :

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Supprimer une adresse IP privée statique d’une machine virtuelle

Vous ne pouvez pas supprimer une adresse IP privée statique à partir d’une carte réseau dans l’interface Azure CLI des déploiements Resource Manager. Vous devez respecter les consignes suivantes :
- Créer une nouvelle carte réseau qui utilise une adresse IP dynamique
- Définir hello NIC sur hello VM hello nouvellement créée de carte réseau. 

toochange hello NIC pour hello machine virtuelle utilisée dans les commandes hello ci-dessus, suivez les étapes de hello ci-dessous.

1. Exécutez hello **créer des cartes réseau du réseau azure** commande toocreate une nouvelle carte réseau à l’aide de l’allocation dynamique d’IP avec une nouvelle adresse IP. Notez que, car aucune adresse IP n’est spécifié, méthode d’allocation de hello est **dynamique**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Sortie attendue :

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Exécutez hello **ensemble de la machine virtuelle azure** commande toochange hello carte réseau utilisée par hello machine virtuelle.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Sortie attendue :
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Si hello machine virtuelle est suffisante toohave plusieurs cartes réseau, exécutez hello **supprimer les cartes réseau du réseau azure** commande hello de toodelete ancien NIC.
   
## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .
* En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .
* Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).

