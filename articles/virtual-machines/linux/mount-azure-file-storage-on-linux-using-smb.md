---
title: "stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB d’aaaMount | Documents Microsoft"
description: "Comment toomount stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB avec hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Monter le stockage de fichiers Azure sur les machines virtuelles Linux à l’aide de SMB

Cet article vous explique comment tooutilize hello service de stockage Azure sur un VM Linux à l’aide d’un serveur SMB montage avec hello Azure CLI 2.0. Stockage de fichiers Azure offre des partages de fichiers dans le cloud hello à l’aide du protocole SMB standard de hello. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). spécifications de Hello sont :

- [un compte Azure](https://azure.microsoft.com/pricing/free-trial/)
- [des fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>Commandes rapides

* Un groupe de ressources.
* Un réseau virtuel Azure.
* Un groupe de sécurité réseau avec une connexion SSH entrante.
* Un sous-réseau.
* Un compte de stockage Azure.
* Des clés de compte de stockage Azure.
* Un partage de stockage de fichiers Azure.
* Une machine virtuelle Linux.

Remplacez les exemples par vos propres paramètres.

### <a name="create-a-directory-for-hello-local-mount"></a>Créez un répertoire de montage local de hello

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Monter le point de montage hello fichier stockage SMB partage toohello

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Conserver le montage de hello après un redémarrage
toodo, ajoutez hello suivant ligne toohello `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

Stockage de fichiers offre des partages de fichiers dans le cloud de hello qui utilisent le protocole SMB standard de hello. Avec la version la plus récente hello de stockage de fichiers, vous pouvez également monter un partage de fichiers à partir de n’importe quel système d’exploitation qui prend en charge SMB 3.0. Lorsque vous utilisez un montage SMB sur Linux, vous obtenez sauvegardes tooa robustes et permanente d’archivage emplacement de stockage qui est pris en charge par un contrat SLA.

Déplacement des fichiers à partir d’un montage SMB tooan machine virtuelle qui est hébergé sur le stockage de fichiers est qu'un excellent moyen toodebug se connecte. C’est parce que hello partage SMB même peut être monté localement tooyour Mac, Linux ou Windows station de travail. SMB n’est pas la meilleure solution pour Linux de diffusion en continu de hello ou de journaux des applications en temps réel, car hello protocole SMB n’est pas généré toohandle ces droits journalisation lourde. Un outil de couche de journalisation unifié et dédié comme Fluentd resprésente un meilleur choix que SMB pour collecter la sortie de journalisation d’applications et Linux.

Pour cette procédure pas à pas détaillées, nous créer les conditions préalables à hello nécessaires toofirst création du partage de stockage de fichier hello et puis montez via SMB sur un VM Linux.

1. Créer un groupe de ressources avec [création de groupe de az](/cli/azure/group#create) partage de fichiers toohold hello.

    toocreate un groupe de ressources nommé `myResourceGroup` Bonjour emplacement de « Ouest des États-Unis », utilisez hello l’exemple suivant :

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Créer un compte Azure storage avec [créer de compte de stockage az](/cli/azure/storage/account#create) toostore hello fichiers réels.

    toocreate un compte de stockage nommé mystorageaccount en utilisant le stockage hello Standard_LRS référence (SKU), hello d’utiliser l’exemple suivant :

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Afficher les clés de compte de stockage hello.

    Lorsque vous créez un compte de stockage, les clés de compte hello sont créés dans les paires afin qu’ils peuvent être pivotées sans aucune interruption de service. Lorsque vous basculez toohello deuxième clé de la paire de hello, vous créez une nouvelle paire de clés. Nouvelles clés de compte de stockage sont toujours créés par paires, s’assurer que vous disposez toujours au moins un tooswitch prêt clé stockage inutilisés compte à.

    Afficher les clés de compte de stockage hello avec hello [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list). Hello clés de compte de stockage pour hello nommé `mystorageaccount` sont répertoriées dans hello l’exemple suivant :

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract une clé unique, utiliser hello `--query` indicateur. première clé de hello extrait Hello suivant (`[0]`) :

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Création du partage de stockage de fichier hello.

    partage de fichiers de stockage Hello contient hello partage SMB avec [créer de partage de stockage az](/cli/azure/storage/share#create). quota de Hello est toujours exprimée en gigaoctets (Go). Passez l’une des clés de hello de hello précédent `az storage account keys list` commande. Créer un partage nommé mystorageshare avec un quota de 10 Go à l’aide de hello l’exemple suivant :

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Créez un répertoire de point de montage.

    Créer un répertoire local dans hello toomount hello Linux fichier système partage SMB. Rien écrire ou lire à partir du répertoire de montage local hello est transféré toohello partage SMB qui est hébergé sur le stockage de fichiers. toocreate un répertoire local sur/mnt/mymountdirectory, hello d’utiliser l’exemple suivant :

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Montez le répertoire local du toohello partage SMB hello.

    Fournissez votre propre nom d’utilisateur du compte de stockage et de la clé de compte de stockage pour les informations d’identification de montage hello comme suit :

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Hello SMB de montage de redémarrages de persistance.

    Lorsque vous redémarrez hello Linux VM, hello monté partage SMB est démonté lors de l’arrêt. hello tooremount partage SMB sur le démarrage, ajouter une ligne de toohello/etc/fstab Linux. Linux utilise hello fstab fichier toolist hello systèmes de fichiers qu’il doit toomount pendant le processus de démarrage hello. Ajouter le partage SMB hello garantit que ce partage de stockage de fichier hello est un système de fichiers monté définitivement pour hello Linux VM. Hello fichier stockage SMB partage tooa nouvel ordinateur virtuel est possible d’ajouter lorsque vous utilisez init-cloud.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Étapes suivantes

- [Lors de la création à l’aide de cloud-init toocustomize un VM Linux](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Ajouter un tooa de disque Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Chiffrer les disques sur un VM Linux à l’aide de hello CLI d’Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
