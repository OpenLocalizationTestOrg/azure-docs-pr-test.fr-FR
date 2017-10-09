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
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="b2fb3-103">Création et téléchargement d’un disque dur virtuel qui contient hello système d’exploitation Linux</span><span class="sxs-lookup"><span data-stu-id="b2fb3-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b2fb3-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b2fb3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b2fb3-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b2fb3-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b2fb3-107">Vous pouvez également [charger une image de disque personnalisé à l’aide d’Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2fb3-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b2fb3-108">Cet article vous explique comment toocreate et téléchargez un disque dur virtuel (VHD) afin de pouvoir l’utiliser comme votre propre image toocreate machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="b2fb3-109">Découvrez comment tooprepare hello d’exploitation système, vous pouvez l’utiliser toocreate plusieurs machines virtuelles en fonction de cette image.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="b2fb3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b2fb3-110">Prerequisites</span></span>
<span data-ttu-id="b2fb3-111">Cet article suppose que vous avez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="b2fb3-112">**Système d’exploitation Linux dans un fichier .vhd** -vous avez installé un [distribution Linux d’approuvées Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consultez [concernant des distributions non approuvées](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) disque virtuel de tooa dans le format de disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="b2fb3-113">Plusieurs outils existent toocreate une machine virtuelle et le disque dur virtuel :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="b2fb3-114">Installer et configurer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), en prenant soin de toouse disque dur virtuel en tant que format de votre image.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="b2fb3-115">Vous pouvez [convertir une image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) à l’aide de `qemu-img convert` si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="b2fb3-116">Vous pouvez également utiliser Hyper-V [sur Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [sur Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2fb3-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b2fb3-117">nouveau format VHDX de Hello n’est pas pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="b2fb3-118">Lorsque vous créez une machine virtuelle, spécifiez le disque dur virtuel en tant que format de hello.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="b2fb3-119">Si nécessaire, vous pouvez convertir à l’aide de tooVHD de disques VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="b2fb3-120">En outre, Azure ne prend pas en charge téléchargement de disques durs virtuels dynamiques, par conséquent, vous devez tooconvert ce toostatic disques vhd avant de télécharger.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="b2fb3-121">Vous pouvez utiliser des outils tels que [utilitaires de disque dur virtuel de Azure pour atteindre](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert les disques dynamiques pendant le processus hello de téléchargement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="b2fb3-122">**Interface de ligne de commande Azure** -hello installation dernières [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello de tooupload disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="b2fb3-123"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="b2fb3-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="b2fb3-124">Étape 1 : Préparer hello image toobe est téléchargé</span><span class="sxs-lookup"><span data-stu-id="b2fb3-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="b2fb3-125">Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="b2fb3-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="b2fb3-126">Hello suivant articles vous guide tout au long de la tooprepare hello diverses distributions Linux prises en charge sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="b2fb3-127">Après avoir terminé les étapes de hello Bonjour guides de, revenez ici une fois que vous avez un fichier de disque dur virtuel est prêt tooupload tooAzure :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="b2fb3-128">**[Distributions CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b2fb3-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b2fb3-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b2fb3-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b2fb3-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b2fb3-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b2fb3-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b2fb3-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b2fb3-132">**[SLES et openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b2fb3-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b2fb3-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b2fb3-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b2fb3-134">**[Autres - Distributions non approuvées](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b2fb3-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="b2fb3-135">Hello SLA de la plateforme Azure s’applique à des ordinateurs toovirtual hello Linux OS uniquement lorsqu’une des hello visé distributions est utilisé avec les détails de configuration hello comme indiqué dans la section « Prise en charge des Versions » en cours d’exécution [Azure-Endorsed Distributions Linux sur ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2fb3-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b2fb3-136">Toutes les distributions de Linux dans la galerie d’images Azure hello sont distributions visées avec la configuration requise de hello.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="b2fb3-137">Voir aussi hello  **[Notes d’Installation Linux](../create-upload-generic.md#general-linux-installation-notes)**  pour obtenir des conseils plus générales sur la préparation d’images Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="b2fb3-138"><a id="connect"></a></span><span class="sxs-lookup"><span data-stu-id="b2fb3-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="b2fb3-139">Étape 2 : Préparer hello connexion tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2fb3-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="b2fb3-140">Vérifiez que vous utilisez hello CLI d’Azure dans le modèle de déploiement classique hello (`azure config mode asm`), puis connectez-vous à tooyour compte :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="b2fb3-141"><a id="upload"></a></span><span class="sxs-lookup"><span data-stu-id="b2fb3-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="b2fb3-142">Étape 3 : Téléchargez hello image tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2fb3-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="b2fb3-143">Vous devez un tooupload de compte de stockage pour votre fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="b2fb3-144">Vous pouvez choisir un compte de stockage existant ou [en créer un](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b2fb3-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="b2fb3-145">Utiliser des images de hello tooupload hello CLI d’Azure à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="b2fb3-146">Dans l’exemple précédent de hello :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-146">In hello previous example:</span></span>

* <span data-ttu-id="b2fb3-147">**BlobStorageURL** est hello URL hello compte de stockage vous envisagez de toouse</span><span class="sxs-lookup"><span data-stu-id="b2fb3-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="b2fb3-148">**YourImagesFolder** est conteneur hello dans le stockage d’objets blob dans lequel vous souhaitez que toostore vos images</span><span class="sxs-lookup"><span data-stu-id="b2fb3-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="b2fb3-149">**VHDName** hello étiquette qui apparaît dans le portail tooidentify hello un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="b2fb3-150">**PathToVHDFile** est le chemin d’accès complet de hello et nom du fichier de disque dur virtuel hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="b2fb3-151">Hello commande suivante illustre un exemple complet :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="b2fb3-152">Étape 4 : Créer une machine virtuelle à partir de l’image de hello</span><span class="sxs-lookup"><span data-stu-id="b2fb3-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="b2fb3-153">Vous créez une machine virtuelle à l’aide `azure vm create` Bonjour comme une machine virtuelle standard.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="b2fb3-154">Spécifiez le nom de hello vous donnez votre image à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="b2fb3-155">Bonjour l’exemple suivant, nous utilisons hello **myImage** nom de l’image donné dans l’étape précédente de hello :</span><span class="sxs-lookup"><span data-stu-id="b2fb3-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="b2fb3-156">toocreate vos propres machines virtuelles, fournissez votre propre nom d’utilisateur + mot de passe, l’emplacement, nom DNS et nom de l’image.</span><span class="sxs-lookup"><span data-stu-id="b2fb3-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2fb3-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2fb3-157">Next steps</span></span>
<span data-ttu-id="b2fb3-158">Pour plus d’informations, consultez [référence CLI d’Azure pour le modèle de déploiement classique Azure hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b2fb3-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
