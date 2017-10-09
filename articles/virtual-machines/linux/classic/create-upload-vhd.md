---
title: "aaaCreate et télécharger un tooAzure Linux VHD | Documents Microsoft"
description: "Créer et télécharger un Azure disque dur virtuel (VHD) qui contient le système d’exploitation de hello Linux à l’aide du modèle de déploiement classique de hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Création et téléchargement d’un disque dur virtuel qui contient hello système d’exploitation Linux
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Vous pouvez également [charger une image de disque personnalisé à l’aide d’Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Cet article vous explique comment toocreate et téléchargez un disque dur virtuel (VHD) afin de pouvoir l’utiliser comme votre propre image toocreate machines virtuelles Azure. Découvrez comment tooprepare hello d’exploitation système, vous pouvez l’utiliser toocreate plusieurs machines virtuelles en fonction de cette image. 


## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez hello éléments suivants :

* **Système d’exploitation Linux dans un fichier .vhd** -vous avez installé un [distribution Linux d’approuvées Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consultez [concernant des distributions non approuvées](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) disque virtuel de tooa dans le format de disque dur virtuel hello. Plusieurs outils existent toocreate une machine virtuelle et le disque dur virtuel :
  * Installer et configurer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), en prenant soin de toouse disque dur virtuel en tant que format de votre image. Vous pouvez [convertir une image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) à l’aide de `qemu-img convert` si nécessaire.
  * Vous pouvez également utiliser Hyper-V [sur Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [sur Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> nouveau format VHDX de Hello n’est pas pris en charge dans Azure. Lorsque vous créez une machine virtuelle, spécifiez le disque dur virtuel en tant que format de hello. Si nécessaire, vous pouvez convertir à l’aide de tooVHD de disques VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) applet de commande PowerShell. En outre, Azure ne prend pas en charge téléchargement de disques durs virtuels dynamiques, par conséquent, vous devez tooconvert ce toostatic disques vhd avant de télécharger. Vous pouvez utiliser des outils tels que [utilitaires de disque dur virtuel de Azure pour atteindre](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert les disques dynamiques pendant le processus hello de téléchargement tooAzure.

* **Interface de ligne de commande Azure** -hello installation dernières [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello de tooupload disque dur virtuel.

<a id="prepimage"></a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>Étape 1 : Préparer hello image toobe est téléchargé
Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hello suivant articles vous guide tout au long de la tooprepare hello diverses distributions Linux prises en charge sur Azure. Après avoir terminé les étapes de hello Bonjour guides de, revenez ici une fois que vous avez un fichier de disque dur virtuel est prêt tooupload tooAzure :

* **[Distributions CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES et openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Autres - Distributions non approuvées](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> Hello SLA de la plateforme Azure s’applique à des ordinateurs toovirtual hello Linux OS uniquement lorsqu’une des hello visé distributions est utilisé avec les détails de configuration hello comme indiqué dans la section « Prise en charge des Versions » en cours d’exécution [Azure-Endorsed Distributions Linux sur ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Toutes les distributions de Linux dans la galerie d’images Azure hello sont distributions visées avec la configuration requise de hello.
> 
> 

Voir aussi hello  **[Notes d’Installation Linux](../create-upload-generic.md#general-linux-installation-notes)**  pour obtenir des conseils plus générales sur la préparation d’images Linux pour Azure.

<a id="connect"></a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>Étape 2 : Préparer hello connexion tooAzure
Vérifiez que vous utilisez hello CLI d’Azure dans le modèle de déploiement classique hello (`azure config mode asm`), puis connectez-vous à tooyour compte :

```azurecli
azure login
```


<a id="upload"></a>

## <a name="step-3-upload-hello-image-tooazure"></a>Étape 3 : Téléchargez hello image tooAzure
Vous devez un tooupload de compte de stockage pour votre fichier de disque dur virtuel. Vous pouvez choisir un compte de stockage existant ou [en créer un](../../../storage/common/storage-create-storage-account.md).

Utiliser des images de hello tooupload hello CLI d’Azure à l’aide de hello de commande suivante :

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

Dans l’exemple précédent de hello :

* **BlobStorageURL** est hello URL hello compte de stockage vous envisagez de toouse
* **YourImagesFolder** est conteneur hello dans le stockage d’objets blob dans lequel vous souhaitez que toostore vos images
* **VHDName** hello étiquette qui apparaît dans le portail tooidentify hello un disque dur virtuel.
* **PathToVHDFile** est le chemin d’accès complet de hello et nom du fichier de disque dur virtuel hello sur votre ordinateur.

Hello commande suivante illustre un exemple complet :

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>Étape 4 : Créer une machine virtuelle à partir de l’image de hello
Vous créez une machine virtuelle à l’aide `azure vm create` Bonjour comme une machine virtuelle standard. Spécifiez le nom de hello vous donnez votre image à l’étape précédente de hello. Bonjour l’exemple suivant, nous utilisons hello **myImage** nom de l’image donné dans l’étape précédente de hello :

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate vos propres machines virtuelles, fournissez votre propre nom d’utilisateur + mot de passe, l’emplacement, nom DNS et nom de l’image.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez [référence CLI d’Azure pour le modèle de déploiement classique Azure hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
