---
title: "aaaUpload une image personnalisée de Linux avec Azure CLI 1.0 | Documents Microsoft"
description: "Créez et téléchargez un disque dur virtuel (VHD) de tooAzure avec une image personnalisée de Linux à l’aide du modèle de déploiement du Gestionnaire de ressources hello et hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="efa61-103">Télécharger et de créer un VM Linux à partir de l’image de disque personnalisé à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="efa61-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="efa61-104">Cet article explique comment tooupload un tooAzure de disque dur virtuel (VHD) à l’aide de hello du modèle de déploiement de gestionnaire de ressources et comment créer des machines virtuelles Linux à partir de cette image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="efa61-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="efa61-105">Cette fonctionnalité vous permet de tooinstall et configurer les exigences de tooyour distribution de Linux et ensuite utiliser ce disque dur virtuel tooquickly créer des machines virtuelles (VM).</span><span class="sxs-lookup"><span data-stu-id="efa61-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="efa61-106">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="efa61-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="efa61-107">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="efa61-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="efa61-108">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="efa61-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="efa61-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="efa61-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="efa61-110">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="efa61-110">Quick commands</span></span>
<span data-ttu-id="efa61-111">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section tooupload des commandes de base un tooAzure de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="efa61-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="efa61-112">Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#requirements).</span><span class="sxs-lookup"><span data-stu-id="efa61-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="efa61-113">Assurez-vous que vous avez [hello Azure CLI 1.0](../../cli-install-nodejs.md) connecté et l’utilisation du mode de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="efa61-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="efa61-114">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="efa61-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="efa61-115">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myimages`.</span><span class="sxs-lookup"><span data-stu-id="efa61-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="efa61-116">Créez d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="efa61-116">First, create a resource group.</span></span> <span data-ttu-id="efa61-117">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `WestUs` emplacement :</span><span class="sxs-lookup"><span data-stu-id="efa61-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="efa61-118">Créer un toohold de compte de stockage de vos disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="efa61-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="efa61-119">Hello exemple suivant crée un compte de stockage nommé `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="efa61-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="efa61-120">Liste des clés d’accès hello pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="efa61-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="efa61-121">Notez la valeur de `key1` :</span><span class="sxs-lookup"><span data-stu-id="efa61-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="efa61-122">Créer un conteneur au sein de votre compte de stockage à l’aide de la clé de stockage hello obtenu.</span><span class="sxs-lookup"><span data-stu-id="efa61-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="efa61-123">Hello exemple suivant crée un conteneur nommé `myimages` à l’aide de la valeur de clé de stockage hello de `key1`:</span><span class="sxs-lookup"><span data-stu-id="efa61-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="efa61-124">Enfin, téléchargez votre conteneur de toohello disque dur virtuel que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="efa61-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="efa61-125">Spécifier le chemin d’accès local de hello tooyour disque dur virtuel sous `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="efa61-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="efa61-126">Vous pouvez maintenant créer une machine virtuelle à partir de votre disque virtuel chargé [à l’aide d’un modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="efa61-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="efa61-127">Vous pouvez également utiliser hello CLI en spécifiant le disque de hello URI tooyour (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="efa61-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="efa61-128">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide du disque virtuel de hello téléchargé précédemment :</span><span class="sxs-lookup"><span data-stu-id="efa61-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="efa61-129">compte de stockage de destination Hello a toobe même hello comme où vous avez téléchargé votre disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="efa61-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="efa61-130">Également toospecify, ou que vous demande de répondre, tous les hello paramètres supplémentaires requis par hello `azure vm create` commande comme réseau virtuel, adresse IP publique, nom d’utilisateur et les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="efa61-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="efa61-131">Vous pouvez en savoir plus sur hello [paramètres disponibles de gestionnaire de ressources CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="efa61-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="efa61-132">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="efa61-132">Requirements</span></span>
<span data-ttu-id="efa61-133">toocomplete hello comme suit, vous devez :</span><span class="sxs-lookup"><span data-stu-id="efa61-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="efa61-134">**Système d’exploitation Linux dans un fichier .vhd** -installer un [distribution Linux d’approuvées Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consultez [plus d’informations pour les distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa de disque virtuel Bonjour disque dur virtuel format.</span><span class="sxs-lookup"><span data-stu-id="efa61-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="efa61-135">Plusieurs outils existent toocreate une machine virtuelle et le disque dur virtuel :</span><span class="sxs-lookup"><span data-stu-id="efa61-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="efa61-136">Installer et configurer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), en prenant soin de toouse disque dur virtuel en tant que format de votre image.</span><span class="sxs-lookup"><span data-stu-id="efa61-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="efa61-137">Vous pouvez [convertir une image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) à l’aide de `qemu-img convert` si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="efa61-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="efa61-138">Vous pouvez également utiliser Hyper-V [sur Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [sur Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="efa61-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="efa61-139">nouveau format VHDX de Hello n’est pas pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="efa61-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="efa61-140">Lorsque vous créez une machine virtuelle, spécifiez le disque dur virtuel en tant que format de hello.</span><span class="sxs-lookup"><span data-stu-id="efa61-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="efa61-141">Si nécessaire, vous pouvez convertir à l’aide de tooVHD de disques VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efa61-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="efa61-142">En outre, Azure ne prend pas en charge téléchargement de disques durs virtuels dynamiques, par conséquent, vous devez tooconvert ce toostatic disques vhd avant de télécharger.</span><span class="sxs-lookup"><span data-stu-id="efa61-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="efa61-143">Vous pouvez utiliser des outils tels que [utilitaires de disque dur virtuel de Azure pour atteindre](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert les disques dynamiques pendant le processus hello de téléchargement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="efa61-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="efa61-144">Machines virtuelles créées à partir de votre image personnalisée doivent se trouver dans hello même compte de stockage en tant qu’image hello lui-même</span><span class="sxs-lookup"><span data-stu-id="efa61-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="efa61-145">Créer un toohold de compte et conteneur de stockage de votre image personnalisée et les machines virtuelles créées</span><span class="sxs-lookup"><span data-stu-id="efa61-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="efa61-146">Après avoir créé toutes vos machines virtuelles, vous pouvez supprimer votre image en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="efa61-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="efa61-147">Assurez-vous que vous avez [hello Azure CLI 1.0](../../cli-install-nodejs.md) connecté et l’utilisation du mode de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="efa61-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="efa61-148">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="efa61-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="efa61-149">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myimages`.</span><span class="sxs-lookup"><span data-stu-id="efa61-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="efa61-150"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="efa61-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="efa61-151">Préparer hello image toobe est téléchargé</span><span class="sxs-lookup"><span data-stu-id="efa61-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="efa61-152">Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="efa61-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="efa61-153">Hello suivant articles vous guide tout au long de la tooprepare hello diverses distributions Linux prises en charge sur Azure :</span><span class="sxs-lookup"><span data-stu-id="efa61-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="efa61-154">**[Distributions CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="efa61-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="efa61-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="efa61-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="efa61-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="efa61-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="efa61-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="efa61-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="efa61-158">**[SLES et openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="efa61-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="efa61-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="efa61-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="efa61-160">**[Autres - Distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="efa61-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="efa61-161">Voir aussi hello  **[Notes d’Installation Linux](create-upload-generic.md#general-linux-installation-notes)**  pour obtenir des conseils plus générales sur la préparation d’images Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="efa61-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="efa61-162">Hello [la plateforme Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applique tooVMs Linux en cours d’exécution lorsque un des hello visé distributions est utilisé uniquement avec les détails de configuration hello comme indiqué dans la section « Prise en charge des Versions » en [Linux sur Azure approuvées Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efa61-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="efa61-163">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="efa61-163">Create a resource group</span></span>
<span data-ttu-id="efa61-164">Groupes de ressources logiquement réunissent tous les toosupport de ressources Azure hello vos machines virtuelles, telles que les réseaux virtuels hello et de stockage.</span><span class="sxs-lookup"><span data-stu-id="efa61-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="efa61-165">Découvrez plus d’informations sur les [groupes de ressources Azure ici](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="efa61-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="efa61-166">Avant de télécharger l’image de disque personnalisée et création de machines virtuelles, vous devez d’abord toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="efa61-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="efa61-167">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `WestUS` emplacement :</span><span class="sxs-lookup"><span data-stu-id="efa61-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="efa61-168">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="efa61-168">Create a storage account</span></span>
<span data-ttu-id="efa61-169">Les machines virtuelles sont stockées en tant qu’objets blob de pages au sein d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="efa61-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="efa61-170">Découvrez plus d’informations sur [Azure Storage ici](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="efa61-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="efa61-171">Vous créez un compte de stockage pour votre image de disque personnalisée et vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="efa61-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="efa61-172">Les machines virtuelles que vous créez à partir de votre toobe de nécessité d’image disque personnalisé dans hello même compte de stockage en tant que cette image.</span><span class="sxs-lookup"><span data-stu-id="efa61-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="efa61-173">Hello exemple suivant crée un compte de stockage nommé `mystorageaccount` dans le groupe de ressources hello créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="efa61-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="efa61-174">Répertorier les clés de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="efa61-174">List storage account keys</span></span>
<span data-ttu-id="efa61-175">Azure génère deux clés d’accès de 512 bits pour chaque compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="efa61-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="efa61-176">Ces clés d’accès sont utilisées lors de l’authentification de compte de stockage toohello, telles que toocarry les opérations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="efa61-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="efa61-177">En savoir plus sur [la gestion des accès toostorage ici](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="efa61-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="efa61-178">Vous pouvez afficher les touches d’accès rapide par hello `azure storage account keys list` commande.</span><span class="sxs-lookup"><span data-stu-id="efa61-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="efa61-179">Afficher les touches d’accès hello pour le compte de stockage hello créé :</span><span class="sxs-lookup"><span data-stu-id="efa61-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="efa61-180">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="efa61-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="efa61-181">Prenez note de `key1` comme vous l’utiliserez toointeract avec votre compte de stockage dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="efa61-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="efa61-182">Créer un conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="efa61-182">Create a storage container</span></span>
<span data-ttu-id="efa61-183">Bonjour même façon que vous créez des répertoires différents toologically organiser votre système de fichiers local, vous créez des conteneurs dans un tooorganize de compte de stockage des disques virtuels et des images.</span><span class="sxs-lookup"><span data-stu-id="efa61-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="efa61-184">Un compte de stockage peut contenir un certain nombre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="efa61-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="efa61-185">Hello exemple suivant crée un conteneur nommé `myimages`, en spécifiant la clé d’accès hello obtenu à l’étape précédente de hello (`key1`) :</span><span class="sxs-lookup"><span data-stu-id="efa61-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="efa61-186">Charger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="efa61-186">Upload VHD</span></span>
<span data-ttu-id="efa61-187">Désormais, vous pouvez charger votre image de disque personnalisée.</span><span class="sxs-lookup"><span data-stu-id="efa61-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="efa61-188">Comme pour tous les disques virtuels utilisés par les machines virtuelles, vous devez charger et stocker votre image de disque personnalisée en tant qu’objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="efa61-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="efa61-189">Spécifiez votre clé d’accès, le conteneur hello créé à l’étape précédente de hello, puis hello image de disque personnalisée toohello de chemin d’accès sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="efa61-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="efa61-190">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="efa61-190">Create VM from custom image</span></span>
<span data-ttu-id="efa61-191">Lorsque vous créez des machines virtuelles à partir de l’image de disque personnalisé, spécifiez l’image de disque toohello hello URI.</span><span class="sxs-lookup"><span data-stu-id="efa61-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="efa61-192">Vérifiez que hello correspondances de compte de stockage de destination où est stockée votre image personnalisée de disque.</span><span class="sxs-lookup"><span data-stu-id="efa61-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="efa61-193">Vous pouvez créer votre machine virtuelle à l’aide de hello CLI d’Azure ou le Gestionnaire de ressources JSON d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="efa61-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="efa61-194">Créer une machine virtuelle à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="efa61-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="efa61-195">Vous spécifiez hello `--image-urn` paramètre hello `azure vm create` image de disque personnalisé commande toopoint tooyour.</span><span class="sxs-lookup"><span data-stu-id="efa61-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="efa61-196">Vérifiez que `--storage-account-name` correspondances hello compte de stockage où est stockée votre image personnalisée de disque.</span><span class="sxs-lookup"><span data-stu-id="efa61-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="efa61-197">Il est inutile toouse hello même conteneur comme hello toostore d’image de disque personnalisé à vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="efa61-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="efa61-198">Assurez-vous que toocreate tous les conteneurs Bonjour comme hello des étapes précédentes avant de télécharger vos images de disques personnalisées.</span><span class="sxs-lookup"><span data-stu-id="efa61-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="efa61-199">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à partir de l’image de disque personnalisé :</span><span class="sxs-lookup"><span data-stu-id="efa61-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="efa61-200">Toujours toospecify, ou que vous demande de répondre, tous les hello paramètres supplémentaires requis par hello `azure vm create` commande comme réseau virtuel, adresse IP publique, nom d’utilisateur et les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="efa61-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="efa61-201">En savoir plus sur hello [paramètres disponibles de gestionnaire de ressources CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="efa61-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="efa61-202">Créer une machine virtuelle à l’aide d’un modèle JSON</span><span class="sxs-lookup"><span data-stu-id="efa61-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="efa61-203">Les modèles de gestionnaire de ressources Azure sont des fichiers JavaScript Objet Notation (JSON) qui définissent l’environnement hello toobuild vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="efa61-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="efa61-204">modèles de Hello sont réparties dans les fournisseurs de ressources toodifferent tels que compute ou réseau.</span><span class="sxs-lookup"><span data-stu-id="efa61-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="efa61-205">Vous pouvez utiliser les modèles existants ou écrire les vôtres.</span><span class="sxs-lookup"><span data-stu-id="efa61-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="efa61-206">Découvrez plus d’informations sur [l’utilisation des modèles et de Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="efa61-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="efa61-207">Au sein de hello `Microsoft.Compute/virtualMachines` fournisseur de votre modèle, vous avez un `storageProfile` nœud qui contient les détails de configuration hello pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="efa61-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="efa61-208">Hello deux principaux paramètres tooedit sont hello `image` et `vhd` URI qui pointent image de disque personnalisée tooyour et disque virtuel de votre nouvelle VM.</span><span class="sxs-lookup"><span data-stu-id="efa61-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="efa61-209">suivant de Hello montre un exemple Hello JSON pour l’utilisation d’une image de disque personnalisé :</span><span class="sxs-lookup"><span data-stu-id="efa61-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="efa61-210">Vous pouvez utiliser [cette toocreate modèle existant une machine virtuelle à partir d’une image personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou consultez l’article sur [créer vos propres modèles Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="efa61-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="efa61-211">Une fois que vous avez un modèle configuré, vous créez vos machines virtuelles à l’aide de hello `azure group deployment create` commande.</span><span class="sxs-lookup"><span data-stu-id="efa61-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="efa61-212">Spécifiez hello URI de votre modèle de JSON avec hello `--template-uri` paramètre :</span><span class="sxs-lookup"><span data-stu-id="efa61-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="efa61-213">Si vous avez un fichier JSON stocké localement sur votre ordinateur, vous pouvez utiliser hello `--template-file` paramètre à la place :</span><span class="sxs-lookup"><span data-stu-id="efa61-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="efa61-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="efa61-214">Next steps</span></span>
<span data-ttu-id="efa61-215">Après avoir préparé et chargé votre disque virtuel personnalisé, vous pouvez découvrir plus d’informations sur [l’utilisation de Resource Manager et des modèles](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="efa61-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="efa61-216">Vous pouvez également trop[ajouter un disque de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="efa61-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="efa61-217">Si vous avez des applications en cours d’exécution sur vos ordinateurs virtuels que vous avez besoin de tooaccess, veillez trop[ouvrir les ports et les points de terminaison](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efa61-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

