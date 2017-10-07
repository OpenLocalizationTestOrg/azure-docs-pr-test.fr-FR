---
title: aaaExpand des disques durs virtuels sur un VM Linux dans Azure | Documents Microsoft
description: "Découvrez comment tooexpand des disques durs virtuels sur un VM Linux avec hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Comment tooexpand des disques durs virtuels sur un VM Linux avec hello CLI d’Azure
taille de disque dur virtuel par défaut Hello hello système d’exploitation (OS) est généralement 30 Go sur un ordinateur virtuel de Linux (VM) dans Azure. Vous pouvez [ajouter des disques de données](add-disk.md) tooprovide d’espace de stockage supplémentaire, mais vous souhaiterez également tooexpand un disque de données existant. Cet article décrit en détail comment tooexpand des disques gérés pour un VM Linux avec hello Azure CLI 2.0. Vous pouvez également développer le disque de système d’exploitation hello non managée avec hello [Azure CLI 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Assurez-vous de toujours sauvegarder vos données avant de redimensionner des disques. Pour plus d’informations, consultez [Back up Linux VMs in Azure](tutorial-backup-vms.md) (Sauvegarder des machines virtuelles Linux dans Azure).

## <a name="expand-disk"></a>Développer le disque
Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Cet article nécessite une machine virtuelle existante dans Azure avec au moins un disque de données attaché et préparé. Si vous n’avez pas encore de machine virtuelle à utiliser, consultez [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks) (Créer et préparer une machine virtuelle avec des disques de données).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup* et *myVM*.

1. Opérations sur les disques durs virtuels ne peuvent pas être effectuées avec hello machine virtuelle en cours d’exécution. Libérez la machine virtuelle avec la commande [az vm deallocate](/cli/azure/vm#deallocate). exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`ne libère pas de ressources de calcul hello. toorelease des ressources de calcul, utilisez `az vm deallocate`. Hello machine virtuelle doit être libérée tooexpand hello un disque dur virtuel.

2. Affichez la liste des disques gérés dans un groupe de ressources avec la commande [az disk list](/cli/azure/disk#list). Hello exemple suivant affiche une liste de disques gérés dans le groupe de ressources hello nommé *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Développez disque hello avec [mise à jour du disque az](/cli/azure/disk#update). exemple Hello développe managé disque hello *myDataDisk* toobe *200*Go :

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Lorsque vous développez un disque géré, taille de hello mis à jour est mappé toohello plus proche de la taille de disque géré. Pour un tableau des tailles de disque géré disponible hello et les niveaux, consultez [présentation des disques Azure géré - tarification et facturation](../windows/managed-disks-overview.md#pricing-and-billing).

3. Démarrez votre machine virtuelle avec [az vm start](/cli/azure/vm#start). Hello après le démarrage de l’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour machine virtuelle avec les informations d’identification appropriées hello. Vous pouvez obtenir hello adresse IP publique de votre machine virtuelle avec [afficher de machine virtuelle az](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. toouse hello développé de disque, vous devez système de fichiers et de la partition de tooexpand hello sous-jacente.

    a. Si déjà monté, démontez le disque de hello :

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Utilisez `parted` tooview informations de disque et redimensionner hello partition :

    ```bash
    sudo parted /dev/sdc
    ```

    Afficher des informations sur la disposition de partition existant hello avec `print`. la sortie est similaire toohello suivant exemple, qui affiche la taille de disque sous-jacent de hello est 215 Go Hello :

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Développez la partition hello avec `resizepart`. Entrez le numéro de partition hello, *1*et une taille pour la nouvelle partition de hello :

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, entrez`quit`

5. Avec partition hello redimensionnée, vérifiez la cohérence de partition hello avec `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Désormais redimensionner filesystem hello avec `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Montage hello partition toohello souhaité emplacement, tel que `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. disque de hello du système d’exploitation tooverify a été redimensionné, utilisez `df -h`. Hello après la sortie de l’exemple montre le lecteur de données hello, *sdc1/dev/*, est maintenant de 200 Go :

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Étapes suivantes
Si vous avez besoin de stockage supplémentaire, vous également [ajouter des disques de données tooa Linux VM](add-disk.md). Pour plus d’informations sur le chiffrement de disque, consultez [crypter les disques sur un VM Linux à l’aide de hello CLI d’Azure](encrypt-disks.md).
