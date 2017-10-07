---
title: "aaaManage Azure disques avec hello CLI d’Azure | Documents Microsoft"
description: "Didacticiel - gérer les disques Azure avec hello CLI d’Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Gérer les disques Azure avec hello CLI d’Azure

Machines virtuelles Azure utilisent le système d’exploitation de disques toostore hello machines virtuelles, des applications et des données. Lorsque vous créez une machine virtuelle, il est important toochoose une taille de disque et la charge de travail de configuration approprié toohello attendu. Ce didacticiel décrit le déploiement et la gestion des disques de machine virtuelle. Vous en apprendrez davantage sur les points suivants :

> [!div class="checklist"]
> * Disques de système d’exploitation et disques temporaires
> * Disques de données
> * Disques Standard et Premium
> * Performances des disques
> * Attachement et préparation des disques de données
> * Redimensionnement des disques
> * Captures instantanées de disque


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Disques Azure par défaut

Création d’une machine virtuelle Azure, deux disques sont automatiquement attaché toohello virtual machine. 

**Disque de système d’exploitation** - disques de système d’exploitation peuvent être dimensionnés des téraoctets de too1 et hôtes hello de système d’exploitation de machines virtuelles. disque de Hello du système d’exploitation est étiqueté */dev/sda* par défaut. disque Hello mise en cache de la configuration du disque du système d’exploitation hello est optimisé pour les performances du système d’exploitation. En raison de cette configuration, hello disque de système d’exploitation **ne doivent pas** héberger des applications ou des données. Pour héberger ce type de contenu, utilisez plutôt des disques de données, qui sont décrits plus loin dans cet article. 

**Disque temporaire** -les disques temporaires utilisent un disque SSD qui se trouve sur hello même hôte Azure en tant que machine virtuelle de hello. Les disques temporaires sont extrêmement performants et peuvent être utilisés pour des opérations telles que le traitement de données temporaires. Toutefois, si hello machine virtuelle est déplacée tooa nouvel hôte, toutes les données stockées sur un disque temporaire sont supprimées. taille de Hello du disque temporaire de hello est déterminé par hello taille de machine virtuelle. Les disques temporaires sont nommés */dev/sdb* et ont un point de montage */mnt*.

### <a name="temporary-disk-sizes"></a>Tailles du disque temporaire

| Type | Taille de la machine virtuelle | Taille maximale du disque temporaire (Go) |
|----|----|----|
| [Usage général](sizes-general.md) | Séries A et D | 800 |
| [Optimisé pour le calcul](sizes-compute.md) | Série F | 800 |
| [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md) | Séries D et G | 6144 |
| [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md) | Série L | 5630 |
| [GPU](sizes-gpu.md) | Série N | 1 440 |
| [Hautes performances](sizes-hpc.md) | Séries A et H | 2000 |

## <a name="azure-data-disks"></a>Disques de données Azure

Des disques de données supplémentaires peuvent être ajoutés pour installer des applications et stocker des données. Les disques de données doivent être utilisés dans les cas où un stockage des données durable et réactif est souhaité. Chaque disque de données possède une capacité maximale de 1 To. taille de Hello de machine virtuelle de hello détermine le nombre de disques de données peut être attaché tooa machine virtuelle. Pour chaque cœur de la machine virtuelle, deux disques de données peuvent être attachés. 

### <a name="max-data-disks-per-vm"></a>Disques de données max. par machine virtuelle

| Type | Taille de la machine virtuelle | Disques de données max. par machine virtuelle |
|----|----|----|
| [Usage général](sizes-general.md) | Séries A et D | 32 |
| [Optimisé pour le calcul](sizes-compute.md) | Série F | 32 |
| [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md) | Séries D et G | 64 |
| [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md) | Série L | 64 |
| [GPU](sizes-gpu.md) | Série N | 48 |
| [Hautes performances](sizes-hpc.md) | Séries A et H | 32 |

## <a name="vm-disk-types"></a>Type de disque de machine virtuelle

Azure propose deux types de disque.

### <a name="standard-disk"></a>Disque Standard

Le stockage Standard s’appuie sur des disques durs et offre un stockage économique qui n’en est pas moins performant. Les disques Standard constituent la solution idéale pour une charge de travail de développement et de test économique.

### <a name="premium-disk"></a>Disque Premium

Les disques Premium reposent sur un disque SSD à faible latence et hautes performances. Ils conviennent parfaitement aux machines virtuelles exécutant une charge de travail en production. Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS et FS. Les disques Premium sont fournis dans les trois types (P10, P20, P30), taille hello du disque de hello détermine le type de disque hello. Lors de la sélection, une valeur de hello de taille de disque est arrondie toohello les type suivant. Par exemple, si la taille du disque hello est inférieure à 128 Go, le type de disque hello est P10. Si la taille du disque hello est comprise entre 129 et 512 Go, taille de hello est un P20. Tout élément plus de 512 Go, taille de hello est un P30.

### <a name="premium-disk-performance"></a>Performances du disque Premium

|Type de disque de stockage Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Taille du disque (arrondie) | 128 Go | 512 Go | 1 024 Go (1 To) |
| Nb max. d'E/S par seconde par disque | 500 | 2 300 | 5 000 |
Débit par disque | 100 Mo/s | 150 Mo/s | 200 Mo/s |

Tandis que hello au-dessus de table identifie max IOPS par disque, un niveau plus élevé de performances est possible par l’agrégation de plusieurs disques de données. Par exemple, une machine virtuelle Standard_GS5 peut atteindre un nombre maximum d’E/S par seconde de 80 000. Pour plus d’informations sur le nombre max. d’E/S par seconde par machine virtuelle, consultez [Tailles des machines virtuelles Linux dans Azure](sizes.md).

## <a name="create-and-attach-disks"></a>Créer et attacher des disques

Disques de données peuvent être créés et attachés au moment de la création de machine virtuelle ou tooan existant de machine virtuelle.

### <a name="attach-disk-at-vm-creation"></a>Attacher le disque lors de la création d’une machine virtuelle

Créer un groupe de ressources avec hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) commande. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Créer une machine virtuelle à l’aide de hello [az vm créer]( /cli/azure/vm#create) commande. Hello `--datadisk-sizes-gb` argument est utilisé toospecify qu’un disque supplémentaire doit être créé et attaché toohello virtual machine. toocreate et attacher plusieurs disques, utilisez une liste délimitée par l’espace de valeurs de taille de disque. Bonjour l’exemple suivant, un ordinateur virtuel est créé avec des disques de données de deux, les deux 128 Go. Les tailles de disque hello étant 128 Go, ces disques sont tous deux configurés en tant que P10s, qui fournissent des 500 IOPS maximales par disque.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Attacher le disque tooexisting machine virtuelle

toocreate et attacher une disque tooan existant machine virtuelle, utilisez hello [attacher de disque de machine virtuelle az](/cli/azure/vm/disk#attach) commande. Hello exemple suivant crée un disque premium, 128 Go de taille et l’attache toohello que machine virtuelle créée dans la dernière étape de hello.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Préparer les disques de données

Une fois qu’un disque a été attaché toohello virtual machine, le système d’exploitation de hello doit toobe configuré toouse hello disque. Bonjour à l’exemple suivant montre comment toomanually configurer un disque. Ce processus peut également être automatisé à l’aide de cloud-init, qui est présenté dans un [prochain didacticiel](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configuration manuelle

Créer une connexion SSH avec l’ordinateur virtuel de hello. Remplacez l’exemple d’adresse IP hello avec l’adresse IP publique de l’ordinateur virtuel de hello hello.

```azurecli-interactive 
ssh 52.174.34.95
```

Partition de disque hello avec `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Écrire une partition toohello à l’aide de hello `mkfs` commande.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Monter le disque de nouveau hello afin qu’il soit accessible dans le système d’exploitation de hello.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

disque de Hello sont maintenant accessibles via hello *datadrive* point de montage, ce qui peut être vérifié en exécutant hello `df -h` commande. 

```bash
df -h
```

sortie de Hello affiche hello nouveau lecteur monté sur */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure qui hello lecteur est remontée après un redémarrage, il doit être ajouté toohello */etc/fstab* fichier. toodo par conséquent, obtenir hello UUID de disque de hello avec hello `blkid` utilitaire.

```bash
sudo -i blkid
```

sortie de Hello affiche hello UUID du lecteur de hello `/dev/sdc1` dans ce cas.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Ajouter un toohello similaire de ligne suivant toohello */etc/fstab* fichier. Notez également que la fonctionnalité permettant d’écrire des barrières peut être désactivée à l’aide de *barrier=0*, cette configuration peut améliorer les performances de disque. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Maintenant que hello disque a été configuré, fermez la session SSH de hello.

```bash
exit
```

## <a name="resize-vm-disk"></a>Redimensionner le disque de machine virtuelle

Une fois qu’un ordinateur virtuel a été déployé, disque de système d’exploitation hello ou les disques de données attaché peuvent être augmentées la taille. L’augmentation de taille hello d’un disque est utile lorsque vous avez besoin de davantage d’espace de stockage ou un niveau plus élevé de performances (P10, P20, P30). Notez que vous ne pouvez pas réduire la taille des disques.

Avant d’augmenter la taille du disque, hello Id ou nom du disque de hello est nécessaire. Hello d’utilisation [liste des disques az](/cli/azure/vm/disk#list) tooreturn commande tous les disques dans un groupe de ressources. Prenez note du nom du disque hello que vous aimeriez tooresize.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Hello machine virtuelle doit également être libéré. Hello d’utilisation [az vm désallouer]( /cli/azure/vm#deallocate) commande toostop et désallouer hello machine virtuelle.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Hello d’utilisation [mise à jour du disque az](/cli/azure/vm/disk#update) disque de commande tooresize hello. Cet exemple redimensionne un disque nommé *myDataDisk* too1 téraoctet.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Une fois l’opération de redimensionnement hello terminée, démarrer hello machine virtuelle.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Si vous avez redimensionné hello d’exploitation du disque système, partition de hello est automatiquement développé. Si vous avez redimensionné un disque de données, toutes les partitions en cours doivent toobe développée dans le système d’exploitation de machines virtuelles hello.

## <a name="snapshot-azure-disks"></a>Prendre une capture instantanée des disques Azure

Un instantané de disque crée une copie uniquement, point-à-temps lecture du disque de hello. Les instantanés de machine virtuelle Azure sont utiles pour rapidement enregistrer l’état de hello d’une machine virtuelle avant d’apporter des modifications de configuration. En cas de hello hello modifications de configuration révèle toobe indésirables, état de la machine virtuelle peut être restaurée à l’aide de la capture instantanée de hello. Lorsqu’un ordinateur virtuel possède plusieurs disques, un instantané de chaque disque indépendamment hello d’autres. Pour effectuer des sauvegardes cohérentes d’application, envisagez l’arrêt hello machine virtuelle avant d’effectuer des captures instantanées de disque. Vous pouvez également utiliser hello [service Azure Backup](/azure/backup/), qui permet aux vous tooperform automatisée sauvegardes hello machine virtuelle est en cours d’exécution.

### <a name="create-snapshot"></a>Création d’un instantané

Avant de créer un instantané de disque de machine virtuelle, hello Id ou nom de disque de hello est nécessaire. Hello d’utilisation [afficher de machine virtuelle az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id de commande tooreturn hello disque. Dans cet exemple, l’id du disque hello est stocké dans une variable afin qu’il peut être utilisé dans une étape ultérieure.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Maintenant que vous avez id hello du disque de machine virtuelle hello, hello commande suivante crée un instantané du disque de hello.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Création d’un disque à partir d’une capture instantanée

Cet instantané peut ensuite être converti en un disque, ce qui peut être utilisé toorecreate hello virtual machine.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Restauration de la machine virtuelle à partir de l’instantané

récupération de machine virtuelle toodemonstrate, ordinateur virtuel existant de suppression hello. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Créer un nouvel ordinateur virtuel à partir du disque de capture instantanée hello.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Rattacher un disque de données

Tous les disques de données doivent toobe rattaché toohello virtual machine.

Tout d’abord rechercher nom hello de disque de données à l’aide de hello [liste des disques az](https://docs.microsoft.com/cli/azure/disk#list) commande. Cet exemple place hello nom du disque hello dans une variable nommée *datadisk*, qui est utilisé dans l’étape suivante de hello.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Hello d’utilisation [attacher de disque de machine virtuelle az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disque de commande tooattach hello.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous a apporté des connaissances concernant les disques de machine virtuelle, notamment concernant les points suivants :

> [!div class="checklist"]
> * Disques de système d’exploitation et disques temporaires
> * Disques de données
> * Disques Standard et Premium
> * Performances des disques
> * Attachement et préparation des disques de données
> * Redimensionnement des disques
> * Captures instantanées de disque

Avance toohello toolearn de didacticiel suivant sur l’automatisation de configuration d’ordinateur virtuel.

> [!div class="nextstepaction"]
> [Automatiser la configuration de machine virtuelle](./tutorial-automate-vm-deployment.md)
