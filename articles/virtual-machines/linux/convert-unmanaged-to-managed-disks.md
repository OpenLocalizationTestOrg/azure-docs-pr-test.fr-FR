---
title: "aaaConvert une machine virtuelle de Linux dans Azure du code non disques toomanaged disques - Azure géré | Documents Microsoft"
description: "Comment tooconvert un VM Linux à partir de disques non managé toomanaged disques à l’aide d’Azure CLI 2.0 dans le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Convertir une machine virtuelle Linux à partir de disques toomanaged de disques non managé

Si vous avez existant Linux virtual machines virtuelles qui utilisent des disques non managés, vous pouvez convertir les disques de toouse géré de machines virtuelles de hello via hello [disques gérés d’Azure](../windows/managed-disks-overview.md) service. Ce processus convertit le disque de hello du système d’exploitation et les disques de données attaché.

Cet article vous explique comment tooconvert machines virtuelles à l’aide de hello CLI d’Azure. Si vous avez besoin de tooinstall ou mettre à niveau, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Avant de commencer

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Convertir des machines virtuelles à instance unique
Cette section explique comment des machines virtuelles Azure à partir de non managé à instance unique de tooconvert disques toomanaged disques. (Si vos machines virtuelles sont dans un ensemble de disponibilité, voir section suivante de hello). Vous pouvez utiliser cette disques toostandard géré de disques de machines virtuelles à partir de disques de toopremium géré disques premium (SSD) non managée, ou à partir de la norme (HDD) non managées processus tooconvert hello.

1. Désallouer hello machine virtuelle à l’aide de [az vm désallouer](/cli/azure/vm#deallocate). exemple Hello désalloue hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Convertir les disques de toomanaged hello machine virtuelle à l’aide de [az vm convertir](/cli/azure/vm#convert). Hello suivant convertit des processus hello ordinateur virtuel nommé `myVM`, y compris les disques hello du système d’exploitation et les disques de données :

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Démarrer hello machine virtuelle une fois les disques toomanaged hello conversion à l’aide de [début de machine virtuelle az](/cli/azure/vm#start). Hello après le démarrage de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Convertir des machines virtuelles dans un groupe à haute disponibilité

Si hello machines virtuelles que vous souhaitez tooconvert toomanaged disques se trouvent dans un ensemble de disponibilité, vous devez commencer tooconvert hello disponibilité ensemble tooa géré à haute disponibilité.

Tous les ordinateurs virtuels dans le groupe à haute disponibilité hello doivent être libérées avant de convertir hello à haute disponibilité. Tooconvert plan tous les disques toomanaged de machines virtuelles après la disponibilité de hello définir elle-même a été converti tooa géré à haute disponibilité. Ensuite, démarrez tous les ordinateurs virtuels de hello et continue à fonctionner normalement.

1. Répertoriez toutes les machines virtuelles contenues dans un groupe à haute disponibilité à l’aide de la commande [az vm availability-set list](/cli/azure/vm/availability-set#list). Hello exemple suivant répertorie toutes les machines virtuelles hello groupe à haute disponibilité nommée `myAvailabilitySet` dans le groupe de ressources hello nommé `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Libérer toutes les machines virtuelles de hello à l’aide de [az vm désallouer](/cli/azure/vm#deallocate). exemple Hello désalloue hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Convertir hello groupe à haute disponibilité à l’aide de [convert de haute-disponibilité az vm](/cli/azure/vm/availability-set#convert). Hello suivant convertit hello groupe à haute disponibilité nommée `myAvailabilitySet` dans le groupe de ressources hello nommé `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Convertir tous les disques de toomanaged hello machines virtuelles à l’aide de [az vm convertir](/cli/azure/vm#convert). Hello suivant convertit des processus hello ordinateur virtuel nommé `myVM`, y compris les disques hello du système d’exploitation et les disques de données :

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Démarrer tous les ordinateurs virtuels de hello après les disques toomanaged hello conversion à l’aide de [début de machine virtuelle az](/cli/azure/vm#start). Hello après le démarrage de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les options de stockage, voir la page [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).
