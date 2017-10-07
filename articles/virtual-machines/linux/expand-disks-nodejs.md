---
title: "disque aaaExpand du système d’exploitation Linux VM par hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooexpand hello le système d’exploitation (OS) de disque virtuel sur un VM Linux à l’aide de hello Azure CLI 1.0 et le modèle de déploiement du Gestionnaire de ressources hello"
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
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Développez le disque du système d’exploitation sur un VM Linux à l’aide de hello CLI d’Azure avec hello Azure CLI 1.0
taille de disque dur virtuel par défaut Hello hello système d’exploitation (OS) est généralement 30 Go sur un ordinateur virtuel de Linux (VM) dans Azure. Vous pouvez [ajouter des disques de données](add-disk.md) tooprovide d’espace de stockage supplémentaire, mais vous souhaiterez peut-être également disque hello du système d’exploitation de tooexpand. Cet article décrit en détail comment tooexpand hello du système d’exploitation du disque pour un VM Linux à l’aide de disques non managés avec hello Azure CLI 1.0.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#prerequisites) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](expand-disks.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="prerequisites"></a>Composants requis
Vous devez hello [dernière Azure CLI 1.0](../../cli-install-nodejs.md) installé et enregistré dans tooan [compte Azure](https://azure.microsoft.com/pricing/free-trial/) en utilisant le mode Gestionnaire de ressources hello comme suit :

```azurecli
azure config mode arm
```

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup* et *myVM*.

## <a name="expand-os-disk"></a>Développer le disque du système d’exploitation

1. Opérations sur les disques durs virtuels ne peuvent pas être effectuées avec hello machine virtuelle en cours d’exécution. Hello exemple suivant arrête et désalloue hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`ne libère pas de ressources de calcul hello. toorelease des ressources de calcul, utilisez `azure vm deallocate`. Hello machine virtuelle doit être libérée tooexpand hello un disque dur virtuel.

2. Mettre à jour de la taille de hello du disque du système d’exploitation hello non managée à l’aide de hello `azure vm set` commande. Hello après les mises à jour de l’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup* toobe *50* Go :

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. Démarrez votre machine virtuelle comme suit :

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour machine virtuelle avec les informations d’identification appropriées hello. disque de hello du système d’exploitation tooverify a été redimensionné, utilisez `df -h`. Hello après la sortie de l’exemple montre la partition principale de hello (*/dev/sda1*) est maintenant de 50 Go :

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Étapes suivantes
Si vous avez besoin de stockage supplémentaire, vous également [ajouter des disques de données tooa Linux VM](add-disk.md). Pour plus d’informations sur le chiffrement de disque, consultez [crypter les disques sur un VM Linux à l’aide de hello CLI d’Azure](encrypt-disks.md).
