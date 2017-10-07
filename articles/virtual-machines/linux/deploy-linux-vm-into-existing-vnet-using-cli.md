---
title: "aaaDeploy les machines virtuelles Linux sur un réseau existant avec Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment une machine virtuelle de Linux dans un réseau virtuel existant à l’aide de toodeploy hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>Comment toodeploy une machine virtuelle de Linux dans un réseau virtuel Azure existant avec hello CLI d’Azure

Cet article vous montre comment toouse hello Azure CLI 2.0 toodeploy un ordinateur virtuel (VM) dans un réseau virtuel existant. spécifications de Hello sont :

- [un compte Azure](https://azure.microsoft.com/pricing/free-trial/)
- [des fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md)

Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Commandes rapides
Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires. Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#detailed-walkthrough).

toocreate cet environnement personnalisé, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.

**Conditions préalables :** groupe de ressources Azure, réseau virtuel et sous-réseau, groupe de sécurité réseau avec SSH entrant et une carte d’interface réseau virtuelle.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Déployer hello VM dans l’infrastructure de réseau virtuel hello

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

Les ressources Azure telles que les réseaux virtuels et les groupes de sécurité réseau doivent être des ressources statiques et durables qui sont rarement déployées. Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives. Réfléchissez à un réseau virtuel comme étant un commutateur de réseau traditionnels matériel - vous ne devez pas tooconfigure basculer d’un nouveau matériel à chaque déploiement. Avec un réseau virtuel configuré correctement, vous pouvez continuer toodeploy nouvelles machines virtuelles dans ce réseau virtuel plusieurs fois avec peu, le cas échéant, modifications requises pendant toute la durée du réseau virtuel de hello hello.

toocreate cet environnement personnalisé, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Commencez par créer un tooorganize de groupe de ressources Azure tout ce que vous créez dans cette procédure pas à pas. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Créer le groupe de ressources hello avec [az groupe créer](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Créer le réseau virtuel de hello

Permet de créer des machines virtuelles dans un hello toolaunch de réseau virtuel Azure. Pour plus d’informations sur les réseaux virtuels, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Créer le réseau virtuel hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create). Hello exemple suivant crée un réseau virtuel nommé *myVnet* et sous-réseau nommé *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Créer un groupe de sécurité réseau hello

Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello. Pour plus d’informations sur les groupes de sécurité réseau, consultez [comment les groupes de sécurité de réseau toocreate Bonjour Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Créer le groupe de sécurité réseau hello avec [az réseau nsg créer](/cli/azure/network/nsg#create). Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Ajouter une règle d’autorisation SSH entrante

Hello machine virtuelle a besoin d’accéder à partir de hello internet, pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello machine virtuelle est nécessaire. Ajouter une règle de trafic entrant pour le groupe de sécurité réseau hello avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create). Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Joindre le groupe de sécurité réseau hello sous-réseau toohello

règles de groupe de sécurité réseau Hello peuvent être appliqué tooa sous-réseau ou une interface de réseau virtuel spécifique. Permet d’attacher le sous-réseau tooour du groupe de sécurité hello réseau. Attacher votre groupe de sécurité réseau de sous-réseau toohello avec [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Ajouter un sous-réseau de réseau virtuel interface carte toohello

Cartes d’interface réseau virtuelle (cartes réseau) sont importantes que vous puissiez les réutiliser en connectant les machines virtuelles de toodifferent. Cette réutilisation permet tookeep hello VNic comme une ressource statique tandis que hello machines virtuelles peut être temporaire. Créer une carte réseau virtuelle et l’associer à sous-réseau hello avec [créer des cartes réseau du réseau az](/cli/azure/network/nic#create). Hello exemple suivant crée une carte réseau virtuelle nommée *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Déployer hello VM dans l’infrastructure de réseau virtuel hello

Vous avez maintenant un réseau virtuel et sous-réseau et un sous-réseau hello tooprotect de groupe de sécurité réseau en bloquant tout le trafic entrant, à l’exception de port 22 pour SSH. Hello machine virtuelle peut désormais être déployé à l’intérieur de cette infrastructure réseau existante.

Créez votre machine virtuelle avec [az vm create](/cli/azure/vm#create). Pour plus d’informations sur hello indicateurs toouse avec hello Azure CLI 2.0 toodeploy une machine virtuelle complète, consultez [créer un environnement complet de Linux à l’aide de hello CLI d’Azure](create-cli-complete.md).

Bonjour à l’exemple suivant crée une machine virtuelle à l’aide de disques gérés d’Azure. Ces disques sont gérées par hello plateforme Azure et ne nécessitent pas de n’importe quel toostore préparation ou emplacement les. Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../../storage/storage-managed-disks-overview.md). Si vous souhaitez les disques toouse non managée, consultez hello supplémentaires Remarque ci-dessous.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Si vous utilisez des disques gérés, ignorez cette étape. Si vous souhaitez les disques toouse non managée, vous devez hello tooadd des paramètres supplémentaires toohello passer commande toocreate non managée disques dans le compte de stockage hello nommé suivants `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

À l’aide de hello CLI indicateurs toocall les ressources existantes, vous indiquez à Azure toodeploy hello machine virtuelle à l’intérieur du réseau existant de hello. Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure. Dans cet exemple, vous ne pas créer et affecter un toohello d’adresse publique IP VNic, cet ordinateur virtuel n’est pas accessible publiquement sur Internet de hello. Pour plus d’informations, consultez [créer une machine virtuelle avec une adresse IP publique statique à l’aide de hello CLI d’Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les machines virtuelles toocreate manières dans Azure, consultez hello suivant des ressources :

* [Utilisez un toocreate de modèle Azure Resource Manager un déploiement spécifique](../windows/cli-deploy-templates.md)
* [Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement](create-cli-complete.md)
* [Création d’une machine virtuelle Linux sur Azure à l’aide de modèles](create-ssh-secured-vm-from-template.md)
