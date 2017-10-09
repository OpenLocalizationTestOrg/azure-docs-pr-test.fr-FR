---
title: "aaaDeploy les machines virtuelles Linux sur un réseau existant avec Azure CLI 1.0 | Documents Microsoft"
description: "Comment un VM Linux dans un réseau virtuel existant à l’aide de toodeploy hello Azure CLI 1.0"
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
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Comment toodeploy une machine virtuelle de Linux dans un réseau virtuel Azure existant avec hello Azure CLI 1.0

Cet article vous montre comment toouse Azure CLI 1.0 toodeploy un ordinateur virtuel (VM) dans un réseau virtuel (VNet). spécifications de Hello sont :

- [un compte Azure](https://azure.microsoft.com/pricing/free-trial/)
- [des fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="quick-commands"></a>Commandes rapides

Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires. Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Configuration requise : groupe de ressources, réseau virtuel, groupe de sécurité réseau avec SSH entrant, sous-réseau. Remplacez les exemples par vos propres paramètres.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Déployer hello VM dans l’infrastructure de réseau virtuel hello

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

Ressources Azure, comme hello des réseaux virtuels et des groupes de sécurité réseau doivent être statiques et de longue durée de vie ressources qui sont rarement déployées. Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives. Voyez les réseaux virtuels comme étant des commutateurs réseau physiques traditionnels. Vous ne devez pas tooconfigure basculer d’un nouveau matériel à chaque déploiement. Avec un réseau virtuel configuré correctement, vous pouvez poursuivre toodeploy nouveaux serveurs dans ce réseau virtuel apportant peu, le cas échéant, de modifications nécessaires pendant toute la durée hello Hello réseau virtuel.

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Commencez par créer un tooorganize de groupe de ressources tout ce que vous créez dans cette procédure pas à pas. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Créer hello réseau virtuel

première étape de Hello est toobuild un toolaunch de réseau virtuel hello des machines virtuelles dans. Hello réseau virtuel contient un sous-réseau pour cette procédure pas à pas. Pour plus d’informations sur des réseaux virtuels Azure, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Créer un groupe de sécurité réseau hello

sous-réseau de Hello repose derrière un groupe de sécurité réseau existant ainsi générer le groupe de sécurité de réseau hello avant le sous-réseau de hello. Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello. Pour plus d’informations sur les groupes de sécurité réseau Azure, consultez [comment les groupes de sécurité de réseau toocreate Bonjour CLI d’Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Ajouter une règle d’autorisation SSH entrante

Hello machine virtuelle a besoin d’accéder à partir de hello internet pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello machine virtuelle est nécessaire.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Ajouter un sous-réseau de toohello réseau virtuel

Machines virtuelles au sein de hello réseau virtuel doivent se trouver dans un sous-réseau. Chaque réseau virtuel peut présenter plusieurs sous-réseaux. Créer hello sous-réseau et l’associer à un groupe de sécurité réseau hello.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Hello sous-réseau est désormais ajouté à l’intérieur de hello réseau virtuel et associé à la règle et le groupe de sécurité réseau hello.


## <a name="add-a-vnic-toohello-subnet"></a>Ajouter un sous-réseau toohello de carte réseau virtuelle

Les cartes réseau virtuelles (cartes réseau) sont importantes que vous puissiez les réutiliser en connectant les machines virtuelles de toodifferent. Cette approche conserve hello VNic comme une ressource statique hello machines virtuelles peut être temporaire. Créer une carte réseau virtuelle et l’associer à sous-réseau hello créé à l’étape précédente de hello.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Déployer hello VM dans hello réseau virtuel et le groupe de sécurité réseau

Vous avez maintenant un réseau virtuel et un sous-réseau à l’intérieur de ce réseau virtuel et un groupe de sécurité réseau font Office de sous-réseau de hello tooprotect en bloque tout le trafic entrant, à l’exception de port 22 pour SSH. Hello machine virtuelle peut désormais être déployé à l’intérieur de cette infrastructure réseau existante.

À l’aide de hello CLI d’Azure et hello `azure vm create` hello Linux VM est déployé toohello existante du groupe de ressources Azure, du réseau virtuel, sous-réseau et une carte réseau virtuelle de la commande. Pour plus d’informations sur l’utilisation de hello CLI toodeploy une machine virtuelle complète, consultez [créer un environnement complet de Linux à l’aide de hello CLI d’Azure](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

À l’aide de hello CLI indicateurs toocall les ressources existantes, vous indiquez à Azure toodeploy hello machine virtuelle à l’intérieur du réseau existant de hello. Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure.  

## <a name="next-steps"></a>Étapes suivantes

* [Utilisez un toocreate de modèle Azure Resource Manager un déploiement spécifique](../windows/cli-deploy-templates.md)
* [Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement](create-cli-complete.md)
* [Création d’une machine virtuelle Linux sur Azure à l’aide de modèles](create-ssh-secured-vm-from-template.md)
