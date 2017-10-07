---
title: "aaaMount stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB avec Azure CLI 1.0 | Documents Microsoft"
description: "Comment toomount stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB"
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
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Montage du Stockage Fichier Azure sur les machines virtuelles Linux à l’aide de SMB avec Azure CLI 1.0

Cet article explique comment toomount stockage de fichier Azure sur un VM Linux à l’aide de hello les protocole Server Message Block (SMB). Stockage de fichiers offre des partages de fichiers dans le cloud hello via le protocole SMB standard hello. spécifications de Hello sont :

* un [compte Azure](https://azure.microsoft.com/pricing/free-trial/) ;
* [des fichiers de clés SSH (Secure Shell) publiques et privées](mac-create-ssh-keys.md).

## <a name="cli-versions-toouse"></a>Toouse des versions CLI
Vous pouvez exécuter la tâche hello en utilisant l’une de hello versions de l’interface de ligne de commande (CLI) suivantes :

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="quick-commands"></a>Commandes rapides
tâche de hello tooaccomplish rapidement, les étapes hello dans cette section. Pour plus d’informations et le contexte, commencent à hello [« Détaillée »](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.

### <a name="prerequisites"></a>Composants requis
* un groupe de ressources ;
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
Ajouter hello suivant ligne trop`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

Stockage de fichiers offre des partages de fichiers dans le cloud de hello qui utilisent le protocole SMB standard de hello. Avec la version la plus récente hello de stockage de fichiers, vous pouvez également monter un partage de fichiers à partir de n’importe quel système d’exploitation qui prend en charge SMB 3.0. Lorsque vous utilisez un montage SMB sur Linux, vous obtenez sauvegardes tooa robustes et permanente d’archivage emplacement de stockage qui est pris en charge par un contrat SLA.

Déplacement des fichiers à partir d’un montage SMB tooan machine virtuelle qui est hébergé sur le stockage de fichiers est qu'un excellent moyen toodebug se connecte. C’est parce que hello partage SMB même peut être monté localement tooyour Mac, Linux ou Windows station de travail. SMB n’est pas la meilleure solution pour Linux de diffusion en continu de hello ou de journaux des applications en temps réel, car hello protocole SMB n’est pas généré toohandle ces droits journalisation lourde. Un outil de couche de journalisation unifié et dédié comme Fluentd resprésente un meilleur choix que SMB pour collecter la sortie de journalisation d’applications et Linux.

Pour cette procédure pas à pas détaillées, nous créer les conditions préalables à hello nécessaires toofirst création du partage de stockage de fichier hello et puis montez via SMB sur un VM Linux.

1. Créer un compte de stockage Azure à l’aide de hello suivant de code :

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Afficher les clés de compte de stockage hello.

    Lorsque vous créez un compte de stockage, les clés de compte hello sont créés dans les paires afin qu’ils peuvent être pivotées sans aucune interruption de service. Lorsque vous basculez toohello deuxième clé de la paire de hello, vous créez une nouvelle paire de clés. Nouvelles clés de compte de stockage sont toujours créés par paires, s’assurer que vous disposez toujours au moins un tooswitch prêt clé stockage inutilisé à. clés de compte de stockage tooshow hello, utilisez hello suivant de code :

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Création du partage de stockage de fichier hello.

    partage de fichiers de stockage Hello contient le partage SMB hello. quota de Hello est toujours exprimée en gigaoctets (Go). toocreate hello du partage de fichiers de stockage, utilisez les hello suivant de code :

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Créer le répertoire de point de montage hello.

    Vous devez créer un répertoire local dans hello toomount hello Linux fichier système partage SMB. Rien écrire ou lire à partir du répertoire de montage local hello est transféré toohello partage SMB qui est hébergé sur le stockage de fichiers. répertoire de hello toocreate, hello utilisation suivante du code :

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. Montez hello partage SMB à l’aide de hello suivant de code :

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Hello SMB de montage de redémarrages de persistance.

    Lorsque vous redémarrez hello Linux VM, hello monté partage SMB est démonté lors de l’arrêt. tooremount le partage SMB hello au démarrage du système, vous devez ajouter une ligne de toohello/etc/fstab Linux. Linux utilise hello fstab fichier toolist hello systèmes de fichiers qu’il doit toomount pendant le processus de démarrage hello. Ajouter le partage SMB hello garantit que ce partage de stockage de fichier hello est un système de fichiers monté définitivement pour hello Linux VM. Hello fichier stockage SMB partage tooa nouvel ordinateur virtuel est possible d’ajouter lorsque vous utilisez init-cloud.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Étapes suivantes

- [Lors de la création à l’aide de cloud-init toocustomize un VM Linux](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Ajouter un tooa de disque Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Chiffrer les disques sur un VM Linux à l’aide de hello CLI d’Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
