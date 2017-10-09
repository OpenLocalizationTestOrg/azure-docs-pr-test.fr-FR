---
title: "aaaUpload un disque Linux personnalisé avec Azure CLI 2.0 | Documents Microsoft"
description: "Créer et télécharger un tooAzure de disque dur virtuel (VHD) à l’aide du modèle de déploiement du Gestionnaire de ressources hello et hello Azure CLI 2.0"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Télécharger et de créer un VM Linux à partir du disque personnalisé avec hello Azure CLI 2.0
Cet article vous montre comment tooupload un tooan de disque dur virtuel (VHD) Azure storage compte avec hello Azure CLI 2.0 et créer des machines virtuelles Linux à partir de ce disque personnalisé. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Cette fonctionnalité vous permet de tooinstall et configurer les exigences de tooyour distribution de Linux et ensuite utiliser ce disque dur virtuel tooquickly créer des machines virtuelles (VM).

Cette rubrique utilise les comptes de stockage pour hello des disques durs virtuels finals, mais vous pouvez également effectuer ces étapes à l’aide de [des disques gérés par](upload-vhd.md). 

## <a name="quick-commands"></a>Commandes rapides
Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section tooupload des commandes de base un tooAzure de disque dur virtuel. Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#requirements).

Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `mydisks`.

Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `WestUs` emplacement :

```azurecli
az group create --name myResourceGroup --location westus
```

Créer un toohold de compte de stockage de vos disques virtuels avec [créer de compte de stockage az](/cli/azure/storage/account#create). Hello exemple suivant crée un compte de stockage nommé `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Liste des clés d’accès hello pour votre compte de stockage avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list). Notez la valeur de `key1` :

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Créer un conteneur au sein de votre compte de stockage à l’aide de la clé de stockage hello que vous avez obtenu avec [créer de conteneur de stockage az](/cli/azure/storage/container#create). Hello exemple suivant crée un conteneur nommé `mydisks` à l’aide de la valeur de clé de stockage hello de `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Enfin, télécharger votre conteneur de toohello disque dur virtuel que vous avez créé avec [téléchargement de blob de stockage az](/cli/azure/storage/blob#upload). Spécifier le chemin d’accès local de hello tooyour disque dur virtuel sous `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Spécifiez hello URI tooyour disque (`--image`) avec [az vm créer](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide du disque virtuel de hello téléchargé précédemment :

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

compte de stockage de destination Hello a toobe même hello comme où vous avez téléchargé votre disque virtuel. Également toospecify, ou que vous demande de répondre, tous les hello paramètres supplémentaires requis par hello **az vm créer** commande comme réseau virtuel, adresse IP publique, nom d’utilisateur et les clés SSH. Vous pouvez en savoir plus sur hello [paramètres disponibles de gestionnaire de ressources CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Configuration requise
toocomplete hello comme suit, vous devez :

* **Système d’exploitation Linux dans un fichier .vhd** -installer un [distribution Linux d’approuvées Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consultez [plus d’informations pour les distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa de disque virtuel Bonjour disque dur virtuel format. Plusieurs outils existent toocreate une machine virtuelle et le disque dur virtuel :
  * Installer et configurer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), en prenant soin de toouse disque dur virtuel en tant que format de votre image. Vous pouvez [convertir une image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) à l’aide de `qemu-img convert` si nécessaire.
  * Vous pouvez également utiliser Hyper-V [sur Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [sur Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> nouveau format VHDX de Hello n’est pas pris en charge dans Azure. Lorsque vous créez une machine virtuelle, spécifiez le disque dur virtuel en tant que format de hello. Si nécessaire, vous pouvez convertir à l’aide de tooVHD de disques VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) applet de commande PowerShell. En outre, Azure ne prend pas en charge téléchargement de disques durs virtuels dynamiques, par conséquent, vous devez tooconvert ce toostatic disques vhd avant de télécharger. Vous pouvez utiliser des outils tels que [utilitaires de disque dur virtuel de Azure pour atteindre](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert les disques dynamiques pendant le processus hello de téléchargement tooAzure.
> 
> 

* Machines virtuelles créées à partir de votre disque personnalisé doivent résider dans hello même compte de stockage comme disque hello lui-même
  * Créer un toohold de compte et conteneur de stockage de vos disques personnalisées et les machines virtuelles créées
  * Après avoir créé toutes vos machines virtuelles, vous pouvez supprimer votre disque en toute sécurité.

Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `mydisks`.

<a id="prepimage"></a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Préparer hello toobe de disque téléchargé
Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hello suivant articles vous guide tout au long de la tooprepare hello diverses distributions Linux prises en charge sur Azure :

* **[Distributions CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES et openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Autres - Distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Voir aussi hello  **[Notes d’Installation Linux](create-upload-generic.md#general-linux-installation-notes)**  pour obtenir des conseils plus générales sur la préparation d’images Linux pour Azure.

> [!NOTE]
> Hello [la plateforme Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applique tooVMs Linux en cours d’exécution lorsque un des hello visé distributions est utilisé uniquement avec les détails de configuration hello comme indiqué dans la section « Prise en charge des Versions » en [Linux sur Azure approuvées Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
Groupes de ressources logiquement réunissent tous les toosupport de ressources Azure hello vos machines virtuelles, telles que les réseaux virtuels hello et de stockage. Pour plus d’informations sur les groupes de ressources, consultez [Présentation des groupes de ressources](../../azure-resource-manager/resource-group-overview.md). Avant de télécharger de votre disque personnalisée et création de machines virtuelles, vous devez toocreate un groupe de ressources avec [az groupe créer](/cli/azure/group#create).

Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement :

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Créez un compte de stockage.

Créez un compte de stockage pour votre disque personnalisé et vos machines virtuelles avec la commande [az storage account create](/cli/azure/storage/account#create). Les machines virtuelles avec des disques non managées que vous créez à partir de votre toobe besoin de disque personnalisé dans hello même compte de stockage en tant que ce disque. 

Hello exemple suivant crée un compte de stockage nommé `mystorageaccount` dans le groupe de ressources hello créé précédemment :

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Répertorier les clés de compte de stockage
Azure génère deux clés d’accès de 512 bits pour chaque compte de stockage. Ces clés d’accès sont utilisées lors de l’authentification de compte de stockage toohello, telles que toocarry les opérations d’écriture. En savoir plus sur [la gestion des accès toostorage ici](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Vous permet d’afficher les clés d’accès hello avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list).

Afficher les touches d’accès hello pour le compte de stockage hello créé :

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Prenez note de `key1` comme vous l’utiliserez toointeract avec votre compte de stockage dans les étapes suivantes hello.

## <a name="create-a-storage-container"></a>Créer un conteneur de stockage
Bonjour même façon que vous créez des répertoires différents toologically organiser votre système de fichiers local, vous créez des conteneurs au sein d’un tooorganize de compte de stockage vos disques. Un compte de stockage peut contenir un certain nombre de conteneurs. Créez un conteneur avec la commande [az storage container create](/cli/azure/storage/container#create).

Hello exemple suivant crée un conteneur nommé `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Charger un disque dur virtuel
Chargez votre disque personnalisé avec la commande [az storage blob upload](/cli/azure/storage/blob#upload). Téléchargez et stockez votre disque personnalisé en tant qu’objet blob de pages.

Spécifiez votre clé d’accès, le conteneur hello créé à l’étape précédente de hello, puis hello disque personnalisé de chemin d’accès toohello sur votre ordinateur local :

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Créer hello machine virtuelle
toocreate une machine virtuelle avec des disques non managés, spécifiez le disque de tooyour hello URI (`--image`) avec [az vm créer](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide du disque virtuel de hello téléchargé précédemment :

Vous spécifiez hello `--image` paramètre avec [az vm créer](/cli/azure/vm#create) disque de toopoint tooyour personnalisé. Vérifiez que `--storage-account` correspondances hello compte de stockage où se trouve votre disque personnalisé. Il est inutile toouse hello même conteneur comme hello disque personnalisé toostore vos machines virtuelles. Assurez-vous que toocreate tous les conteneurs Bonjour comme hello des étapes précédentes avant de télécharger votre disque personnalisé.

Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à partir de votre disque personnalisé :

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Toujours toospecify, ou que vous demande de répondre, tous les hello paramètres supplémentaires requis par hello **az vm créer** commande telles que le nom d’utilisateur et les clés SSH.


## <a name="resource-manager-template"></a>Modèle Resource Manager
Les modèles de gestionnaire de ressources Azure sont des fichiers JavaScript Objet Notation (JSON) qui définissent l’environnement hello toobuild vous le souhaitez. modèles de Hello sont réparties dans les fournisseurs de ressources toodifferent tels que compute ou réseau. Vous pouvez utiliser les modèles existants ou écrire les vôtres. Découvrez plus d’informations sur [l’utilisation des modèles et de Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Au sein de hello `Microsoft.Compute/virtualMachines` fournisseur de votre modèle, vous avez un `storageProfile` nœud qui contient les détails de configuration hello pour votre machine virtuelle. Hello deux principaux paramètres tooedit sont hello `image` et `vhd` URI qui pointent tooyour des disques personnalisées et disque virtuel de votre nouvelle VM. suivant de Hello montre un exemple Hello JSON pour l’utilisation d’un disque personnalisé :

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Vous pouvez utiliser [cette toocreate modèle existant une machine virtuelle à partir d’une image personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou consultez l’article sur [créer vos propres modèles Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Une fois que vous avez un modèle configuré, utilisez [créer de déploiement de groupe az](/cli/azure/group/deployment#create) toocreate vos machines virtuelles. Spécifiez hello URI de votre modèle de JSON avec hello `--template-uri` paramètre :

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Si vous avez un fichier JSON stocké localement sur votre ordinateur, vous pouvez utiliser hello `--template-file` paramètre à la place :

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Étapes suivantes
Après avoir préparé et chargé votre disque virtuel personnalisé, vous pouvez découvrir plus d’informations sur [l’utilisation de Resource Manager et des modèles](../../azure-resource-manager/resource-group-overview.md). Vous pouvez également trop[ajouter un disque de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nouvelles machines virtuelles. Si vous avez des applications en cours d’exécution sur vos ordinateurs virtuels que vous avez besoin de tooaccess, veillez trop[ouvrir les ports et les points de terminaison](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

