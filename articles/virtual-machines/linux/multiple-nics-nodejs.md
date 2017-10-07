---
title: "aaaCreate un VM Linux dans Azure avec plusieurs cartes réseau | Documents Microsoft"
description: "Découvrez comment toocreate un VM Linux avec plusieurs cartes réseau connectée tooit utilisant des modèles de hello CLI d’Azure ou le Gestionnaire de ressources."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>Créer une machine virtuelle Linux avec plusieurs cartes réseau à l’aide de hello Azure CLI 1.0
Vous pouvez créer un ordinateur virtuel (VM) dans Azure qui a plusieurs tooit d’interfaces (NIC) connectées de réseau virtuel. Un scénario courant consiste à toohave des sous-réseaux différents pour la connectivité des serveurs frontale et principaux, ou un réseau dédié tooa analyse ou la solution de sauvegarde. Cet article fournit des commandes rapides toocreate une machine virtuelle avec plusieurs cartes réseau attaché tooit. Pour plus d’informations, y compris comment toocreate Bash plusieurs cartes réseau dans vos propres scripts, en savoir plus sur [déploiement de machines virtuelles multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Comme le nombre de cartes réseau prises en charge varie suivant la [taille des machines virtuelles](sizes.md) , pensez à dimensionner la vôtre en conséquence.

> [!WARNING]
> Vous devez associer plusieurs cartes réseau quand vous créez une machine virtuelle, vous ne pouvez pas ajouter tooan de cartes réseau existantes de machine virtuelle avec hello Azure CLI 1.0. Vous pouvez [ajouter tooan de cartes réseau existantes de machine virtuelle avec hello Azure CLI 2.0](multiple-nics.md). Vous pouvez également [créer une machine virtuelle basée sur des disques virtuels d’origine de hello](copy-vm.md) et créer plusieurs cartes réseau lorsque vous déployez hello machine virtuelle.


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#create-supporting-resources) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](multiple-nics.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="create-supporting-resources"></a>Créer des ressources de support
Assurez-vous que vous avez hello [CLI d’Azure](../../cli-install-nodejs.md) connecté et l’utilisation du mode de gestionnaire de ressources :

```azurecli
azure config mode arm
```

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *mystorageaccount* et *myVM*.

Créez d’abord un groupe de ressources. Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
azure group create myResourceGroup --location eastus
```

Créer un toohold de compte de stockage de vos machines virtuelles. Hello exemple suivant crée un compte de stockage nommé *mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Créer un réseau virtuel de tooconnect vos machines virtuelles. Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec un préfixe d’adresse *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

Créez deux sous-réseaux de réseau virtuel : l’un pour le trafic frontal, l’autre pour le trafic principal. Hello exemple suivant crée deux sous-réseaux, nommés *mySubnetFrontEnd* et *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Créer et configurer plusieurs cartes réseau
Vous trouverez plus d’informations sur les [déploiement de plusieurs cartes réseau à l’aide de hello CLI d’Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), y compris les scripts de processus hello de boucle toocreate toutes les cartes réseau de hello.

Hello exemple suivant crée deux cartes réseau, nommé *myNic1* et *myNic2*, avec une carte réseau qui connectent tooeach sous-réseau :

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

En général, vous créez également un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) ou [l’équilibrage de charge](../../load-balancer/load-balancer-overview.md) toohelp gérer et répartir le trafic entre vos machines virtuelles. Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Lier à votre groupe de sécurité réseau de toohello de cartes réseau à l’aide `azure network nic set`. Hello exemple suivant lie *myNic1* et *myNic2* avec *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Créer une machine virtuelle et d’attachement des cartes réseau de hello
Lorsque vous créez hello machine virtuelle, vous spécifiez maintenant plusieurs cartes réseau. Au lieu de cela à l’aide de `--nic-name` tooprovide une seule carte réseau, vous utilisez `--nic-names` et fournir une liste séparée par des virgules de cartes réseau. Vous devez également tootake attention lorsque vous sélectionnez hello taille de machine virtuelle. Il existe des limites pour le nombre total de hello de cartes réseau que vous pouvez ajouter tooa machine virtuelle. En savoir plus sur les [tailles des machines virtuelles Linux](sizes.md). Hello exemple suivant montre comment toospecify plusieurs cartes réseau, puis sur une machine virtuelle de taille qui prend en charge à l’aide de plusieurs cartes réseau (*Standard_DS2_v2*) :

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a>Créer plusieurs cartes réseau à l’aide de modèles Resource Manager
Les modèles de gestionnaire de ressources Azure utilisent déclarative toodefine de fichiers JSON de votre environnement. Vous pouvez consulter une [vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Les modèles de gestionnaire de ressources fournissent une toocreate de façon plusieurs instances d’une ressource pendant le déploiement, telles que la création de plusieurs cartes réseau. Vous utilisez *copie* nombre de hello toospecify de toocreate d’instances :

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

En savoir plus sur la [création de plusieurs instances à l’aide de *copy*](../../resource-group-create-multiple.md). 

Vous pouvez également utiliser un `copyIndex()` toothen ajouter un nom de ressource tooa nombre, qui vous permet de toocreate `myNic1`, `myNic2`, etc. hello Voici un exemple d’ajout de valeur d’index hello :

```json
"name": "[concat('myNic', copyIndex())]", 
```

Vous pouvez consulter un exemple complet de la [création de plusieurs cartes réseau à l’aide de modèles Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Étapes suivantes
Assurez-vous que tooreview [tailles de Linux VM](sizes.md) lors de la tentative de toocreating une machine virtuelle avec plusieurs cartes réseau. Payer une attention toohello nombre de cartes réseau prend en charge la taille de chaque machine virtuelle. 

Souvenez-vous que vous ne pouvez pas ajouter tooan de cartes réseau supplémentaire existant de machine virtuelle, vous devez créer des toutes les cartes réseau de hello lorsque vous déployez hello machine virtuelle. Prenez soin lors de la planification de votre toomake de déploiements que vous avez toute la connectivité réseau hello requis à partir du début de hello.

