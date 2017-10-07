---
title: "aaaCopy un VM Linux à l’aide d’Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocreate une copie de votre machine virtuelle Linux de Azure à l’aide d’Azure CLI 2.0 et disques gérés."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Créer une copie de machine virtuelle Linux à l’aide d’Azure CLI 2.0 et de disques gérés


Cet article vous explique comment toocreate une copie de votre machine virtuelle Azure (VM) en cours d’exécution à l’aide de Linux hello Azure CLI 2.0 et le modèle de déploiement du Gestionnaire de ressources Azure hello. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Vous pouvez également [charger et créer une machine virtuelle à partir d’un disque dur virtuel](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Composants requis


-   Installer [Azure CLI 2.0](/cli/azure/install-az-cli2)

-   Se connecter tooan compte Azure avec [ouverture de session az](/cli/azure/#login).

-   Avoir un toouse de machine virtuelle Azure en tant que source de hello pour votre copie.

## <a name="step-1-stop-hello-source-vm"></a>Étape 1 : Arrêter l’ordinateur virtuel source de hello


Désallouer la source de hello machine virtuelle à l’aide de [az vm désallouer](/cli/azure/vm#deallocate).
exemple Hello désalloue hello ordinateur virtuel nommé **myVM** dans le groupe de ressources hello **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>Étape 2 : Copier la machine virtuelle de la source hello


toocopy une machine virtuelle, vous créez une copie du disque dur virtuel de sous-jacent hello. Ce processus crée un disque dur virtuel spécialisé de disque géré contient hello même configuration et les paramètres de type hello de machine virtuelle source.

Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md). 

1.  Chaque nom de machine virtuelle et hello de son disque du système d’exploitation avec [liste d’ordinateurs virtuels az](/cli/azure/vm#list). exemple Hello répertorie tous les ordinateurs virtuels dans le groupe de ressources nommé **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Copier une disquette hello en créant un nouveau gérés à l’aide du disque [az créer](/cli/azure/disk#create). Hello exemple suivant crée un disque nommé **myCopiedDisk** hello géré disque nommé **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Vérifiez les disques hello géré désormais dans votre groupe de ressources à l’aide de [liste des disques az](/cli/azure/disk#list). Hello exemple suivant répertorie les disques hello géré dans le groupe de ressources hello nommé **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Ignorer trop[« étape 3 : configurer un réseau virtuel «](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>Étape 3 : Configurer un réseau virtuel


Hello étapes facultatives suivantes créent un nouveau réseau virtuel, un sous-réseau, une adresse IP publique et une carte réseau virtuelle (NIC).

Si vous copiez une machine virtuelle pour le dépannage à des fins ou des déploiements supplémentaires, vous pouvez toouse une machine virtuelle dans un réseau virtuel existant.

Si vous souhaitez toocreate une infrastructure de réseau virtuel pour vos machines virtuelles copiés, suivez hello suivant quelques étapes. Si vous ne souhaitez pas toocreate un réseau virtuel, passez trop[étape 4 : créer une machine virtuelle](#step-4-create-a-vm).

1.  Créer un réseau virtuel de hello à l’aide de [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create). Hello exemple suivant crée un réseau virtuel nommé **myVnet** et un sous-réseau nommé **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Exécutez la commande [az network public-ip create](/cli/azure/network/public-ip#create) pour créer une adresse IP publique. Hello exemple suivant crée une adresse IP publique nommée **myPublicIP** portant le nom DNS de hello de **mypublicdns**. (nom DNS de hello doit être unique, par conséquent, fournissez un nom unique).

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Créer à l’aide de cartes réseau hello [créer des cartes réseau du réseau az](/cli/azure/network/nic#create).
    Hello exemple suivant crée une carte réseau nommée **myNic** toothe joint de **mySubnet** sous-réseau :

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>Étape 4 : Créer une machine virtuelle

Vous pouvez désormais créer une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).

Spécifiez hello copiés toouse disque géré en tant que disque de hello du système d’exploitation (--attacher de disque de système d’exploitation), comme suit :

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Étapes suivantes

toolearn comment toouse CLI d’Azure toomanage votre nouvelle machine virtuelle, consultez [les commandes CLI d’Azure pour hello Azure Resource Manager](../azure-cli-arm-commands.md).
