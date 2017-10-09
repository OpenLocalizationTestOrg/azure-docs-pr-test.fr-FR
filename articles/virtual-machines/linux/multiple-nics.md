---
title: "aaaCreate un VM Linux dans Azure avec plusieurs cartes réseau | Documents Microsoft"
description: "Découvrez comment toocreate un VM Linux avec plusieurs cartes réseau connectée tooit à l’aide de modèles Azure CLI 2.0 ou le Gestionnaire de ressources de hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Comment toocreate une machine virtuelle de Linux dans Azure avec le réseau de plusieurs cartes d’interface
Vous pouvez créer un ordinateur virtuel (VM) dans Azure qui a plusieurs tooit d’interfaces (NIC) connectées de réseau virtuel. Un scénario courant consiste à toohave des sous-réseaux différents pour la connectivité des serveurs frontale et principaux, ou un réseau dédié tooa analyse ou la solution de sauvegarde. Cet article décrit en détail comment toocreate une machine virtuelle avec plusieurs cartes réseau attaché tooit et tooadd ou supprimer des cartes réseau à partir d’une machine virtuelle existante. Pour plus d’informations, y compris comment toocreate Bash plusieurs cartes réseau dans vos propres scripts, en savoir plus sur [déploiement de machines virtuelles multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Comme le nombre de cartes réseau prises en charge varie suivant la [taille des machines virtuelles](sizes.md) , pensez à dimensionner la vôtre en conséquence.

Cet article décrit en détail comment toocreate une machine virtuelle avec plusieurs cartes réseau avec hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Créer des ressources de support
Hello installation dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *mystorageaccount* et *myVM*.

Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

Créer le réseau virtuel hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create). Hello exemple suivant crée un réseau virtuel nommé *myVnet* et sous-réseau nommé *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Créer un sous-réseau pour le trafic de back-end hello avec [créer de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#create). Hello exemple suivant crée un sous-réseau nommé *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Créez un groupe de sécurité réseau avec la commande [az network nsg create](/cli/azure/network/nsg#create). Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Créer et configurer plusieurs cartes réseau
Créez deux cartes réseau avec la commande [az network nic create](/cli/azure/network/nic#create). Hello exemple suivant crée deux cartes réseau, nommé *myNic1* et *myNic2*et connectées, groupe de sécurité réseau hello, avec une carte réseau qui connectent tooeach sous-réseau :

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Créer une machine virtuelle et d’attachement des cartes réseau de hello
Lorsque vous créez hello machine virtuelle, spécifiez des cartes réseau de hello que vous avez créé avec `--nics`. Vous devez également tootake attention lorsque vous sélectionnez hello taille de machine virtuelle. Il existe des limites pour le nombre total de hello de cartes réseau que vous pouvez ajouter tooa machine virtuelle. En savoir plus sur les [tailles des machines virtuelles Linux](sizes.md). 

Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>Ajouter un tooa de carte réseau virtuelle
les étapes précédentes Hello créé une machine virtuelle avec plusieurs cartes réseau. Vous pouvez également ajouter tooan de cartes réseau existantes de machine virtuelle avec hello Azure CLI 2.0. 

Créez une autre carte réseau avec [az network nic create](/cli/azure/network/nic#create). Hello exemple suivant crée une carte réseau nommée *myNic3* connecté sous-réseau principal de toohello et le groupe de sécurité réseau créé dans les étapes précédentes hello :

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd un tooan de carte réseau ordinateur virtuel existant, d’abord libérer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate). exemple Hello désalloue hello ordinateur virtuel nommé *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Ajouter hello carte réseau avec [ajouter de carte réseau de machine virtuelle az](/cli/azure/vm/nic#add). Hello exemple suivant ajoute *myNic3* trop*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Démarrer hello machine virtuelle avec [début de machine virtuelle az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Suppression d’une carte réseau d’une machine virtuelle
tooremove une carte réseau à partir d’un ordinateur virtuel existant, d’abord libérer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate). exemple Hello désalloue hello ordinateur virtuel nommé *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Supprimer hello carte réseau avec [supprimer de la carte réseau de machine virtuelle az](/cli/azure/vm/nic#remove). Hello exemple suivant supprime *myNic3* de *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Démarrer hello machine virtuelle avec [début de machine virtuelle az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
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
Révision [tailles de Linux VM](sizes.md) lors de la tentative de toocreating une machine virtuelle avec plusieurs cartes réseau. Payer une attention toohello nombre de cartes réseau prend en charge la taille de chaque machine virtuelle. 
