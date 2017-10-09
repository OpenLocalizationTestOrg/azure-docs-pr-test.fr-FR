---
title: "aaaUpload ou copier un VM Linux personnalisé avec Azure CLI 2.0 | Documents Microsoft"
description: "Télécharger ou copier un ordinateur virtuel personnalisé à l’aide du modèle de déploiement du Gestionnaire de ressources hello et hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Créer une VM Linux à partir du disque personnalisé avec hello Azure CLI 2.0

<!-- rename toocreate-vm-specialized -->

Cet article vous explique comment tooupload un disque dur virtuel (VHD) personnalisé ou copier un un disque dur virtuel existant dans Azure et créer de nouveaux Linux ordinateurs virtuels (VM) à partir du disque de personnalisée hello. Vous pouvez installer et configurer les exigences de tooyour distribution de Linux et ensuite utiliser ce disque dur virtuel tooquickly créer une machine virtuelle Azure.

Si vous souhaitez toocreate plusieurs machines virtuelles à partir de votre disque personnalisée, vous devez créer une image à partir de votre machine virtuelle ou un disque dur virtuel. Pour plus d’informations, consultez [créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI](tutorial-custom-images.md).

Deux options s'offrent à vous :
* [Charger un disque dur virtuel](#option-1-upload-a-specialized-vhd)
* [Copier une machine virtuelle Azure existante](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Commandes rapides

Lorsque vous créez une nouvelle machine virtuelle en utilisant [az vm créer](/cli/azure/vm#create) à partir d’un disque spécialisé ou personnalisé vous **attacher** disque de hello (--attacher de disque de système d’exploitation) au lieu de spécifier une image personnalisée ou marketplace (--image). Hello exemple suivant crée un ordinateur virtuel nommé *myVM* à l’aide de hello gérés disque nommé *myManagedDisk* créé à partir de votre disque dur virtuel personnalisé :

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Configuration requise
toocomplete hello comme suit, vous devez :

* Une machine virtuelle Linux qui a été préparée pour une utilisation dans Azure. Hello [Prepare hello VM](#prepare-the-vm) section de cet article décrit comment toofind distribution des informations spécifiques sur l’installation de hello Linux Agent Azure (waagent) qui est requis pour toowork de machine virtuelle hello correctement dans Azure et pour vous tooconnect en mesure de toobe tooit à l’aide de SSH.
* fichier de disque dur virtuel Hello d’un existant [distribution Linux d’approuvées Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consultez [plus d’informations pour les distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa de disque virtuel au format de disque dur virtuel de hello. Plusieurs outils existent toocreate une machine virtuelle et le disque dur virtuel :
  * Installer et configurer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), en prenant soin de toouse disque dur virtuel en tant que format de votre image. Vous pouvez [convertir une image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) à l’aide de la commande **qemu-img convert** si nécessaire.
  * Vous pouvez également utiliser Hyper-V [sur Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [sur Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> nouveau format VHDX de Hello n’est pas pris en charge dans Azure. Lorsque vous créez une machine virtuelle, spécifiez le disque dur virtuel en tant que format de hello. Si nécessaire, vous pouvez convertir à l’aide de tooVHD de disques VHDX [qemu-img convertir](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) applet de commande PowerShell. En outre, Azure ne prend pas en charge téléchargement de disques durs virtuels dynamiques, par conséquent, vous devez tooconvert ce toostatic disques vhd avant de télécharger. Vous pouvez utiliser des outils tels que [utilitaires de disque dur virtuel de Azure pour atteindre](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert les disques dynamiques pendant le processus hello de téléchargement tooAzure.
> 
> 


* Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *mystorageaccount* et *mydisks*.

<a id="prepimage"></a>

## <a name="prepare-hello-vm"></a>Préparer hello machine virtuelle

Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hello suivant articles vous guide tout au long de la tooprepare hello diverses distributions Linux prises en charge sur Azure :

* [Distributions CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES et openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Autres - Distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Voir aussi hello [Notes d’Installation Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir des conseils plus générales sur la préparation d’images Linux pour Azure.

> [!NOTE]
> Hello [la plateforme Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applique tooVMs Linux en cours d’exécution lorsque un des hello visé distributions est utilisé uniquement avec les détails de configuration hello comme indiqué dans la section « Prise en charge des Versions » en [Linux sur Azure approuvées Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Option 1 : charger un disque dur virtuel

Vous pouvez charger un disque dur virtuel personnalisé s’exécutant sur un ordinateur local ou que vous avez exporté à partir d’un autre cloud. toocreate de disque dur virtuel hello toouse une machine virtuelle Azure, vous devez stockage tooa de tooupload hello VHD compte et créez un disque géré à partir de hello disque dur virtuel. 

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Avant de télécharger de votre disque personnalisée et création de machines virtuelles, vous devez toocreate un groupe de ressources avec [az groupe créer](/cli/azure/group#create).

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement : [vue d’ensemble de disques gérés d’Azure](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Créez un compte de stockage.

Créez un compte de stockage pour votre disque personnalisé et vos machines virtuelles avec la commande [az storage account create](/cli/azure/storage/account#create). 

Hello exemple suivant crée un compte de stockage nommé *mystorageaccount* dans le groupe de ressources hello créé précédemment :

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Répertorier les clés de compte de stockage
Azure génère deux clés d’accès de 512 bits pour chaque compte de stockage. Ces clés d’accès sont utilisées lors de l’authentification de compte de stockage toohello, comme effectuer des opérations d’écriture. En savoir plus sur [la gestion des accès toostorage ici](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Vous permet d’afficher les clés d’accès hello avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list).

Afficher les touches d’accès hello pour le compte de stockage hello créé :

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

résultat de Hello est similaire à :

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Prenez note de **key1** comme vous l’utiliserez toointeract avec votre compte de stockage dans les étapes suivantes hello.

### <a name="create-a-storage-container"></a>Créer un conteneur de stockage
Bonjour même façon que vous créez des répertoires différents toologically organiser votre système de fichiers local, vous créez des conteneurs au sein d’un tooorganize de compte de stockage vos disques. Un compte de stockage peut contenir un certain nombre de conteneurs. Créez un conteneur avec la commande [az storage container create](/cli/azure/storage/container#create).

Hello exemple suivant crée un conteneur nommé *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Télécharger hello disque dur virtuel
Chargez votre disque personnalisé avec la commande [az storage blob upload](/cli/azure/storage/blob#upload). Téléchargez et stockez votre disque personnalisé en tant qu’objet blob de pages.

Spécifiez votre clé d’accès, le conteneur hello créé à l’étape précédente de hello, puis hello disque personnalisé de chemin d’accès toohello sur votre ordinateur local :

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Téléchargement hello de disque dur virtuel peut prendre un certain temps.

### <a name="create-a-managed-disk"></a>Créer un disque géré


Créer un disque géré à partir de l’aide de disque dur virtuel hello [az créer](/cli/azure/disk#create). Hello exemple suivant crée un disque géré nommé *myManagedDisk* de hello disque dur virtuel, vous avez téléchargé tooyour compte de stockage et de conteneur :

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Option 2 : copier une machine virtuelle existante

Vous pouvez également créer hello personnalisé de machine virtuelle dans Azure, puis copier une disquette hello du système d’exploitation et l’attacher tooa nouvelle machine virtuelle toocreate une autre copie. Cela convient pour le test, mais si vous souhaitez toouse une machine virtuelle Azure existante comme modèle de hello pour plusieurs nouveaux ordinateurs virtuels, vous devez vraiment créer un **image** à la place. Pour plus d’informations sur la création d’une image à partir d’une machine virtuelle Azure existante, consultez [créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Créer un instantané

Cet exemple crée l’instantané d’une machine virtuelle nommée *myVM* dans le groupe de ressources *myResourceGroup* et crée un instantané nommé *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Créer le disque géré de hello

Créer un nouveau disque géré à partir de l’instantané d’hello.

Obtenir l’ID de hello d’instantané de hello. Dans cet exemple, l’instantané d’hello est nommé *osDiskSnapshot* et se trouve dans hello *myResourceGroup* groupe de ressources.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Créer un disque géré de hello. Dans cet exemple, nous allons créer un disque géré nommé *myManagedDisk* à partir de notre instantané, qui représente 128 Go de stockage standard.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Créer hello machine virtuelle

Maintenant, créez votre machine virtuelle avec [az vm créer](/cli/azure/vm#create) et d’attachement (--attacher de disque de système d’exploitation) hello gérés disque comme disque de hello du système d’exploitation. Hello exemple suivant crée un ordinateur virtuel nommé *myNewVM* à l’aide de hello gérés disque créé à partir de votre disque dur virtuel chargé :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Vous devez être en mesure de tooSSH dans hello machine virtuelle à l’aide des informations d’identification hello à partir de l’ordinateur virtuel source de hello. 

## <a name="next-steps"></a>Étapes suivantes
Après avoir préparé et chargé votre disque virtuel personnalisé, vous pouvez découvrir plus d’informations sur [l’utilisation de Resource Manager et des modèles](../../azure-resource-manager/resource-group-overview.md). Vous pouvez également trop[ajouter un disque de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nouvelles machines virtuelles. Si vous avez des applications en cours d’exécution sur vos ordinateurs virtuels que vous avez besoin de tooaccess, veillez trop[ouvrir les ports et les points de terminaison](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

