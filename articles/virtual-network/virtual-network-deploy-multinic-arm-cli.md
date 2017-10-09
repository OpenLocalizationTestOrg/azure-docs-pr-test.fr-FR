---
title: "aaaCreate une machine virtuelle avec plusieurs cartes réseau - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec plusieurs cartes réseau à l’aide de hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Créer une machine virtuelle avec plusieurs cartes réseau à l’aide de hello Azure CLI 2.0

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Créer hello machine virtuelle

Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 2.0 (cet article) ou hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md). Hello dans les valeurs « » pour les variables hello dans les étapes de hello qui suivent créer des ressources avec les paramètres d’un scénario de hello. Modifier les valeurs hello, comme il convient pour votre environnement.

1. Installer hello [Azure CLI 2.0](/cli/azure/install-az-cli2) si vous n’en avez pas encore installé.
2. Créer une paire de clés SSH publique et privée pour les machines virtuelles Linux en effectuant les étapes hello Bonjour [créer une paire de clés SSH publique et privée pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. À partir d’une invite de commandes, la connexion avec la commande hello `az login`.
4. Créer hello machine virtuelle en exécutant le script hello qui suit sur un ordinateur Linux ou Mac. script de Hello crée un groupe de ressources, un réseau virtuel (VNet) avec deux sous-réseaux, deux cartes réseau et une machine virtuelle avec hello deux cartes d’interface réseau attachée tooit. Une des cartes réseau de hello est connecté tooone sous-réseau et est affectée à une adresse IP publique et privée. Hello autre carte réseau est connectée toohello les autres sous-réseaux et reçoit une adresse IP privée statique et aucune adresse IP publique. Hello de carte réseau, adresse IP publique, réseau virtuel et ressources d’ordinateur virtuel doivent tous exister dans hello même emplacement et abonnement. Bien que les ressources hello n’ont pas toutes tooexist Bonjour même groupe de ressources, Bonjour elles font de script suivant.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

En outre toocreating une machine virtuelle avec deux cartes réseau, hello script crée :
- Une prime unique géré disque par défaut, mais vous disposez d’autres options pour le type de disque hello que vous pouvez créer. Hello de lecture [créer un VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article pour plus d’informations.
- Un réseau virtuel avec deux sous-réseaux et une seule adresse IP publique. Vous pouvez également utiliser des ressources *existantes* en matière de réseau virtuel, sous-réseau, carte réseau ou adresse IP publique. toolearn comment toouse existant ressources réseau plutôt que la création de ressources supplémentaires, entrez `az vm create -h`.

## <a name = "validate"></a>Valider la création d’une machine virtuelle et de cartes réseau

1. Entrez la commande hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee une liste de ressources hello créé par un script de hello. Il doit y avoir six ressources Bonjour retourné de sortie : deux cartes réseau, un disque, une adresse IP publique, un réseau virtuel et un ordinateur virtuel.
2. Entrez la commande hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. Bonjour retourné de sortie, notez hello de **IpAddress** et cette valeur hello de **PublicIpAllocationMethod** est *statique*.
3. Avant d’exécuter hello commande suivante, supprimez hello <>, remplacez *nom d’utilisateur* avec nom hello de hello **nom d’utilisateur** variable dans le script de hello, puis remplacez *ipAddress* avec hello **ipAddress** à partir de l’étape précédente de hello. Suivante d’exécution hello commande tooconnect toohello machine virtuelle : `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. Une fois connecté toohello machine virtuelle, exécutez hello `sudo ifconfig` commande toosee *eth0* et *eth1* interfaces. Hello privée des adresses IP statiques spécifiés dans le script de hello par les serveurs DHCP Azure hello a été attribuée à chaque carte réseau. Hello des adresses IP et MAC affectés toohello NIC ne changent pas tant que hello que machine virtuelle est supprimée. Nous vous recommandons de ne pas modifier l’adressage IP dans un système d’exploitation, car il peut désactiver ordinateur toohello de connectivité. Les adresses IP publiques n’apparaissent pas dans le système d’exploitation de hello, lorsqu’ils sont tooand adresse traduite de réseau à partir de l’adresse IP privée de hello en hello infrastructure Azure.

## <a name= "clean-up"></a>Supprimer hello machine virtuelle et les ressources associées

Il est recommandé de supprimer les ressources hello créés dans cet exercice, si vous ne les utilisez en production. La machine virtuelle, l’adresse IP publique et le disque occasionnent des frais tant que ces ressources sont configurées. ressources de hello tooremove créés au cours de cet exercice, hello complète comme suit :
1. tooview hello ressources hello groupe de ressources, exécutez hello `az resource list --resource-group Multi-NIC-VM` commande.
2. Ne vérifiez qu’aucune ressource dans le groupe de ressources hello, autres que les ressources hello créées par script hello dans cet article. 
3. toodelete toutes les ressources créées dans cet exercice, exécutez hello `az group delete --name Multi-NIC-VM` commande. commande Hello supprime le groupe de ressources hello et toutes les ressources hello qu’il contient.

## <a name="next-steps"></a>Étapes suivantes

Tout le trafic réseau peut circuler tooand de hello que machine virtuelle créée dans cet article. Vous pouvez définir des règles entrantes et sortantes au sein d’un groupe de sécurité réseau qui limitent le trafic hello qui peut circuler tooand à partir de chaque interface réseau, chaque sous-réseau ou les deux. toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md) l’article.
