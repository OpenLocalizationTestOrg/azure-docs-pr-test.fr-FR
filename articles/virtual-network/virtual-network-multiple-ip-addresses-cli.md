---
title: "aaaVM avec plusieurs adresses IP à l’aide de hello Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment tooassign des adresses IP multiples à l’aide de machine virtuelle tooa hello Azure CLI 2.0 | Gestionnaire de ressources."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Affecter des ordinateurs toovirtual hello Azure CLI 2.0 à l’aide de plusieurs adresses IP

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Cet article explique comment toocreate un ordinateur virtuel (VM) l’utilisation de modèle de déploiement Azure Resource Manager hello hello Azure CLI 2.0. Tooresources créé via le modèle de déploiement classique hello ne peut pas être assignés à plusieurs adresses IP. toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP

Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 2.0 (cet article) ou hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md). Modifier les valeurs hello, comme il convient pour votre environnement. Hello étapes qui suivent expliquent comment toocreate un exemple de machine virtuelle avec plusieurs IP, les adresses, comme décrit dans le scénario de hello. Modifiez les valeurs des variables entre symboles "" et les types d’adresses IP en fonction des besoins de votre implémentation. 

1. Installer hello [Azure CLI 2.0](/cli/azure/install-az-cli2) si vous n’en avez pas encore installé.
2. Créer une paire de clés SSH publique et privée pour les machines virtuelles Linux en effectuant les étapes hello Bonjour [créer une paire de clés SSH publique et privée pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. À partir d’une invite de commandes, la connexion avec la commande hello `az login` et sélectionnez l’abonnement hello vous utilisez.
4. Créer hello machine virtuelle en exécutant le script hello qui suit sur un ordinateur Linux ou Mac. script de Hello crée un groupe de ressources, un réseau virtuel (VNet), une carte réseau avec trois configurations IP et une machine virtuelle avec hello deux cartes réseau attaché tooit. Hello de carte réseau, adresse IP publique, réseau virtuel et ressources d’ordinateur virtuel doivent tous exister dans hello même emplacement et abonnement. Bien que les ressources hello n’ont pas toutes tooexist Bonjour même groupe de ressources, Bonjour elles font de script suivant.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

En outre toocreating une machine virtuelle avec une carte réseau avec des configurations IP 3, hello script crée :

- Une prime unique géré disque par défaut, mais vous disposez d’autres options pour le type de disque hello que vous pouvez créer. Hello de lecture [créer un VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article pour plus d’informations.
- Un réseau virtuel avec un sous-réseau et deux adresses IP publiques. Vous pouvez également utiliser des ressources *existantes* en matière de réseau virtuel, sous-réseau, carte réseau ou adresse IP publique. toolearn comment toouse existant ressources réseau plutôt que la création de ressources supplémentaires, entrez `az vm create -h`.

Les adresses IP publiques ont un coût nominal. toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.

Après la création de hello machine virtuelle, entrez hello `az network nic show --name MyNic1 --resource-group myResourceGroup` configuration de carte réseau de commande tooview hello. Entrez hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview une liste des configurations IP de hello associés toohello carte

Système d’exploitation de l’ordinateur virtuel toohello les adresses IP privée de hello ajouter en procédant comme hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.

## <a name="add"></a>Ajouter tooa d’adresses IP virtuelle

Vous pouvez ajouter plus privé et public IP adresses tooan existant de carte réseau en effectuant les étapes hello qui suivent. les exemples Hello reposent sur hello [scénario](#Scenario) décrit dans cet article.

1. Ouvrez une invite de commandes et complète hello restant étapes de cette section dans une session unique. Si vous n’avez pas encore installé et configuré CLI d’Azure, hello terminé les étapes Bonjour [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour de connexion et de l’article compte Azure avec hello `az-login` commande.

2. Suivez les étapes de hello dans un des hello les sections, en fonction de vos exigences suivantes :

    **Ajouter une adresse IP privée**
    
    tooadd un tooa d’adresse IP privée carte réseau, vous devez créer une configuration IP à l’aide de la commande hello qui suit. adresse IP statique de Hello doit être une adresse non utilisée pour le sous-réseau de hello.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).

    **Ajouter une adresse IP publique**
    
    Une adresse IP publique est ajoutée en l’associant tooeither une nouvelle configuration IP ou une configuration IP existante. Effectuez les étapes de hello dans une des sections hello qui suivent, dont vous avez besoin.

    Les adresses IP publiques ont un coût nominal. toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.

    - **Associer hello ressource tooa nouvelle configuration IP**
    
        Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée. Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une. toocreate un nouveau, entrez hello de commande suivante :
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        toocreate une nouvelle configuration IP avec une adresse IP privée statique et le hello associés *myPublicIP3* adresse IP publique de ressources d’adresses, entrez hello de commande suivante :

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **Configuration IP existante de hello associer ressource tooan** une ressource d’adresse IP publique peut être uniquement la configuration IP tooan associés qui n’en avez pas encore associé. Vous pouvez déterminer si une configuration IP a une adresse IP publique associée en saisissant hello de commande suivante :

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        Sortie retournée :
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        Depuis hello **PublicIpAddressId** colonne *IpConfig-3* est vide dans hello de sortie, aucune ressource d’adresse IP publique n’est tooit actuellement associé. Vous pouvez ajouter un existant publique IP adresse ressource tooIpConfig-3, ou entrez hello suivant toocreate commande une :

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        Entrez hello commande hello tooassociate adresse IP publique adresse configuration IP existante toohello ressource nommée suivante *IPConfig-3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. Vue hello des adresses IP privées et hello publique d’adresses IP les ID de ressource attribués toohello carte réseau en entrant hello la commande suivante :

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    Sortie retournée : <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Ajouter des adresses IP privées de hello, vous avez ajouté le système d’exploitation VM toohello NIC toohello en suivant les instructions de hello Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresses toohello système d’exploitation.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
