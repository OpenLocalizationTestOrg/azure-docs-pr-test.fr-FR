---
title: aaaCreate une machine virtuelle avec une adresse IP publique statique - Azure CLI 2.0 | Documents Microsoft
description: "Découvrez comment toocreate une machine virtuelle avec un statique publique adresse IP via hello Azure interface de ligne de commande (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Créer une machine virtuelle avec une adresse IP publique statique à l’aide de hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portail Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Modèle](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (classique)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Créer hello machine virtuelle

Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 2.0 (cet article) ou hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). Hello dans les valeurs « » pour les variables hello dans les étapes de hello qui suivent créer des ressources avec les paramètres d’un scénario de hello. Modifier les valeurs hello, comme il convient pour votre environnement.

1. Installer hello [Azure CLI 2.0](/cli/azure/install-az-cli2) si vous n’en avez pas encore installé.
2. Créer une paire de clés SSH publique et privée pour les machines virtuelles Linux en effectuant les étapes hello Bonjour [créer une paire de clés SSH publique et privée pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. À partir d’une invite de commandes, la connexion avec la commande hello `az login`.
4. Créer hello machine virtuelle en exécutant le script hello qui suit sur un ordinateur Linux ou Mac. Hello Azure adresse IP publique, de réseau virtuel, d’interface réseau et ressources d’ordinateur virtuel doivent tous exister dans hello même emplacement. Bien que les ressources hello n’ont pas toutes tooexist Bonjour même groupe de ressources, Bonjour elles font de script suivant.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
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
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

En outre toocreating une machine virtuelle, hello script crée :
- Une prime unique géré disque par défaut, mais vous disposez d’autres options pour le type de disque hello que vous pouvez créer. Hello de lecture [créer un VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article pour plus d’informations.
- Des ressources de réseau virtuel, de sous-réseau, de carte réseau et d’adresse IP publique. Vous pouvez également utiliser des ressources *existantes* en matière de réseau virtuel, sous-réseau, carte réseau ou adresse IP publique. toolearn comment toouse existant ressources réseau plutôt que la création de ressources supplémentaires, entrez `az vm create -h`.

## <a name = "validate"></a>Valider la création de la machine virtuelle et l’adresse IP publique

1. Entrez la commande hello `az resource list --resouce-group IaaSStory --output table` toosee une liste de ressources hello créé par un script de hello. Il doit y avoir cinq ressources Bonjour retourné de sortie : réseau interface, disque, adresse IP publique, réseau virtuel et un ordinateur virtuel.
2. Entrez la commande hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. Bonjour retourné de sortie, notez hello de **IpAddress** et cette valeur hello de **PublicIpAllocationMethod** est *statique*.
3. Avant d’exécuter hello commande suivante, supprimez hello <>, remplacez *nom d’utilisateur* avec nom hello de hello **nom d’utilisateur** variable dans le script de hello, puis remplacez *ipAddress* avec hello **ipAddress** à partir de l’étape précédente de hello. Suivante d’exécution hello commande tooconnect toohello machine virtuelle : `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Supprimer hello machine virtuelle et les ressources associées

Il est recommandé de supprimer les ressources hello créés dans cet exercice, si vous ne les utilisez en production. La machine virtuelle, l’adresse IP publique et le disque occasionnent des frais tant que ces ressources sont configurées. ressources de hello tooremove créés au cours de cet exercice, hello complète comme suit :

1. tooview hello ressources hello groupe de ressources, exécutez hello `az resource list --resource-group IaaSStory` commande.
2. Ne vérifiez qu’aucune ressource dans le groupe de ressources hello, autres que les ressources hello créées par script hello dans cet article. 
3. toodelete toutes les ressources créées dans cet exercice, exécutez hello `az group delete -n IaaSStory` commande. commande Hello supprime le groupe de ressources hello et toutes les ressources hello qu’il contient.

## <a name="next-steps"></a>Étapes suivantes

Tout le trafic réseau peut circuler tooand de hello que machine virtuelle créée dans cet article. Vous pouvez définir des règles entrantes et sortantes au sein d’un groupe de sécurité réseau qui limitent le trafic hello qui peut circuler tooand d’interface réseau de hello, le sous-réseau de hello ou les deux. toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md) l’article.
