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
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="42ef7-103">Télécharger et de créer un VM Linux à partir du disque personnalisé avec hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="42ef7-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="42ef7-104">Cet article vous montre comment tooupload un tooan de disque dur virtuel (VHD) Azure storage compte avec hello Azure CLI 2.0 et créer des machines virtuelles Linux à partir de ce disque personnalisé.</span><span class="sxs-lookup"><span data-stu-id="42ef7-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="42ef7-105">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42ef7-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="42ef7-106">Cette fonctionnalité vous permet de tooinstall et configurer les exigences de tooyour distribution de Linux et ensuite utiliser ce disque dur virtuel tooquickly créer des machines virtuelles (VM).</span><span class="sxs-lookup"><span data-stu-id="42ef7-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="42ef7-107">Cette rubrique utilise les comptes de stockage pour hello des disques durs virtuels finals, mais vous pouvez également effectuer ces étapes à l’aide de [des disques gérés par](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="42ef7-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="42ef7-108">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="42ef7-108">Quick commands</span></span>
<span data-ttu-id="42ef7-109">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section tooupload des commandes de base un tooAzure de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="42ef7-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="42ef7-110">Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#requirements).</span><span class="sxs-lookup"><span data-stu-id="42ef7-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="42ef7-111">Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="42ef7-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="42ef7-112">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="42ef7-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="42ef7-113">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="42ef7-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="42ef7-114">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="42ef7-115">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `WestUs` emplacement :</span><span class="sxs-lookup"><span data-stu-id="42ef7-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="42ef7-116">Créer un toohold de compte de stockage de vos disques virtuels avec [créer de compte de stockage az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="42ef7-117">Hello exemple suivant crée un compte de stockage nommé `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="42ef7-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="42ef7-118">Liste des clés d’accès hello pour votre compte de stockage avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="42ef7-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="42ef7-119">Notez la valeur de `key1` :</span><span class="sxs-lookup"><span data-stu-id="42ef7-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="42ef7-120">Créer un conteneur au sein de votre compte de stockage à l’aide de la clé de stockage hello que vous avez obtenu avec [créer de conteneur de stockage az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="42ef7-121">Hello exemple suivant crée un conteneur nommé `mydisks` à l’aide de la valeur de clé de stockage hello de `key1`:</span><span class="sxs-lookup"><span data-stu-id="42ef7-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="42ef7-122">Enfin, télécharger votre conteneur de toohello disque dur virtuel que vous avez créé avec [téléchargement de blob de stockage az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="42ef7-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="42ef7-123">Spécifier le chemin d’accès local de hello tooyour disque dur virtuel sous `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="42ef7-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="42ef7-124">Spécifiez hello URI tooyour disque (`--image`) avec [az vm créer](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="42ef7-125">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide du disque virtuel de hello téléchargé précédemment :</span><span class="sxs-lookup"><span data-stu-id="42ef7-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="42ef7-126">compte de stockage de destination Hello a toobe même hello comme où vous avez téléchargé votre disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="42ef7-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="42ef7-127">Également toospecify, ou que vous demande de répondre, tous les hello paramètres supplémentaires requis par hello **az vm créer** commande comme réseau virtuel, adresse IP publique, nom d’utilisateur et les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="42ef7-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="42ef7-128">Vous pouvez en savoir plus sur hello [paramètres disponibles de gestionnaire de ressources CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="42ef7-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="42ef7-129">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="42ef7-129">Requirements</span></span>
<span data-ttu-id="42ef7-130">toocomplete hello comme suit, vous devez :</span><span class="sxs-lookup"><span data-stu-id="42ef7-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="42ef7-131">**Système d’exploitation Linux dans un fichier .vhd** -installer un [distribution Linux d’approuvées Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consultez [plus d’informations pour les distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa de disque virtuel Bonjour disque dur virtuel format.</span><span class="sxs-lookup"><span data-stu-id="42ef7-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="42ef7-132">Plusieurs outils existent toocreate une machine virtuelle et le disque dur virtuel :</span><span class="sxs-lookup"><span data-stu-id="42ef7-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="42ef7-133">Installer et configurer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), en prenant soin de toouse disque dur virtuel en tant que format de votre image.</span><span class="sxs-lookup"><span data-stu-id="42ef7-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="42ef7-134">Vous pouvez [convertir une image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) à l’aide de `qemu-img convert` si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="42ef7-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="42ef7-135">Vous pouvez également utiliser Hyper-V [sur Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [sur Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="42ef7-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="42ef7-136">nouveau format VHDX de Hello n’est pas pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="42ef7-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="42ef7-137">Lorsque vous créez une machine virtuelle, spécifiez le disque dur virtuel en tant que format de hello.</span><span class="sxs-lookup"><span data-stu-id="42ef7-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="42ef7-138">Si nécessaire, vous pouvez convertir à l’aide de tooVHD de disques VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42ef7-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="42ef7-139">En outre, Azure ne prend pas en charge téléchargement de disques durs virtuels dynamiques, par conséquent, vous devez tooconvert ce toostatic disques vhd avant de télécharger.</span><span class="sxs-lookup"><span data-stu-id="42ef7-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="42ef7-140">Vous pouvez utiliser des outils tels que [utilitaires de disque dur virtuel de Azure pour atteindre](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert les disques dynamiques pendant le processus hello de téléchargement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="42ef7-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="42ef7-141">Machines virtuelles créées à partir de votre disque personnalisé doivent résider dans hello même compte de stockage comme disque hello lui-même</span><span class="sxs-lookup"><span data-stu-id="42ef7-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="42ef7-142">Créer un toohold de compte et conteneur de stockage de vos disques personnalisées et les machines virtuelles créées</span><span class="sxs-lookup"><span data-stu-id="42ef7-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="42ef7-143">Après avoir créé toutes vos machines virtuelles, vous pouvez supprimer votre disque en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="42ef7-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="42ef7-144">Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="42ef7-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="42ef7-145">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="42ef7-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="42ef7-146">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="42ef7-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="42ef7-147"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="42ef7-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="42ef7-148">Préparer hello toobe de disque téléchargé</span><span class="sxs-lookup"><span data-stu-id="42ef7-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="42ef7-149">Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="42ef7-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="42ef7-150">Hello suivant articles vous guide tout au long de la tooprepare hello diverses distributions Linux prises en charge sur Azure :</span><span class="sxs-lookup"><span data-stu-id="42ef7-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="42ef7-151">**[Distributions CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="42ef7-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="42ef7-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="42ef7-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="42ef7-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="42ef7-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="42ef7-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="42ef7-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="42ef7-155">**[SLES et openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="42ef7-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="42ef7-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="42ef7-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="42ef7-157">**[Autres - Distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="42ef7-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="42ef7-158">Voir aussi hello  **[Notes d’Installation Linux](create-upload-generic.md#general-linux-installation-notes)**  pour obtenir des conseils plus générales sur la préparation d’images Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="42ef7-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="42ef7-159">Hello [la plateforme Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applique tooVMs Linux en cours d’exécution lorsque un des hello visé distributions est utilisé uniquement avec les détails de configuration hello comme indiqué dans la section « Prise en charge des Versions » en [Linux sur Azure approuvées Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42ef7-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="42ef7-160">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="42ef7-160">Create a resource group</span></span>
<span data-ttu-id="42ef7-161">Groupes de ressources logiquement réunissent tous les toosupport de ressources Azure hello vos machines virtuelles, telles que les réseaux virtuels hello et de stockage.</span><span class="sxs-lookup"><span data-stu-id="42ef7-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="42ef7-162">Pour plus d’informations sur les groupes de ressources, consultez [Présentation des groupes de ressources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42ef7-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="42ef7-163">Avant de télécharger de votre disque personnalisée et création de machines virtuelles, vous devez toocreate un groupe de ressources avec [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="42ef7-164">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement :</span><span class="sxs-lookup"><span data-stu-id="42ef7-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="42ef7-165">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="42ef7-165">Create a storage account</span></span>

<span data-ttu-id="42ef7-166">Créez un compte de stockage pour votre disque personnalisé et vos machines virtuelles avec la commande [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="42ef7-167">Les machines virtuelles avec des disques non managées que vous créez à partir de votre toobe besoin de disque personnalisé dans hello même compte de stockage en tant que ce disque.</span><span class="sxs-lookup"><span data-stu-id="42ef7-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="42ef7-168">Hello exemple suivant crée un compte de stockage nommé `mystorageaccount` dans le groupe de ressources hello créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="42ef7-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="42ef7-169">Répertorier les clés de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="42ef7-169">List storage account keys</span></span>
<span data-ttu-id="42ef7-170">Azure génère deux clés d’accès de 512 bits pour chaque compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="42ef7-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="42ef7-171">Ces clés d’accès sont utilisées lors de l’authentification de compte de stockage toohello, telles que toocarry les opérations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="42ef7-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="42ef7-172">En savoir plus sur [la gestion des accès toostorage ici](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="42ef7-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="42ef7-173">Vous permet d’afficher les clés d’accès hello avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="42ef7-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="42ef7-174">Afficher les touches d’accès hello pour le compte de stockage hello créé :</span><span class="sxs-lookup"><span data-stu-id="42ef7-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="42ef7-175">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="42ef7-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="42ef7-176">Prenez note de `key1` comme vous l’utiliserez toointeract avec votre compte de stockage dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="42ef7-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="42ef7-177">Créer un conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="42ef7-177">Create a storage container</span></span>
<span data-ttu-id="42ef7-178">Bonjour même façon que vous créez des répertoires différents toologically organiser votre système de fichiers local, vous créez des conteneurs au sein d’un tooorganize de compte de stockage vos disques.</span><span class="sxs-lookup"><span data-stu-id="42ef7-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="42ef7-179">Un compte de stockage peut contenir un certain nombre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="42ef7-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="42ef7-180">Créez un conteneur avec la commande [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="42ef7-181">Hello exemple suivant crée un conteneur nommé `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="42ef7-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="42ef7-182">Charger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="42ef7-182">Upload VHD</span></span>
<span data-ttu-id="42ef7-183">Chargez votre disque personnalisé avec la commande [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="42ef7-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="42ef7-184">Téléchargez et stockez votre disque personnalisé en tant qu’objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="42ef7-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="42ef7-185">Spécifiez votre clé d’accès, le conteneur hello créé à l’étape précédente de hello, puis hello disque personnalisé de chemin d’accès toohello sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="42ef7-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="42ef7-186">Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="42ef7-186">Create hello VM</span></span>
<span data-ttu-id="42ef7-187">toocreate une machine virtuelle avec des disques non managés, spécifiez le disque de tooyour hello URI (`--image`) avec [az vm créer](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="42ef7-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="42ef7-188">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide du disque virtuel de hello téléchargé précédemment :</span><span class="sxs-lookup"><span data-stu-id="42ef7-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="42ef7-189">Vous spécifiez hello `--image` paramètre avec [az vm créer](/cli/azure/vm#create) disque de toopoint tooyour personnalisé.</span><span class="sxs-lookup"><span data-stu-id="42ef7-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="42ef7-190">Vérifiez que `--storage-account` correspondances hello compte de stockage où se trouve votre disque personnalisé.</span><span class="sxs-lookup"><span data-stu-id="42ef7-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="42ef7-191">Il est inutile toouse hello même conteneur comme hello disque personnalisé toostore vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="42ef7-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="42ef7-192">Assurez-vous que toocreate tous les conteneurs Bonjour comme hello des étapes précédentes avant de télécharger votre disque personnalisé.</span><span class="sxs-lookup"><span data-stu-id="42ef7-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="42ef7-193">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à partir de votre disque personnalisé :</span><span class="sxs-lookup"><span data-stu-id="42ef7-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="42ef7-194">Toujours toospecify, ou que vous demande de répondre, tous les hello paramètres supplémentaires requis par hello **az vm créer** commande telles que le nom d’utilisateur et les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="42ef7-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="42ef7-195">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="42ef7-195">Resource Manager template</span></span>
<span data-ttu-id="42ef7-196">Les modèles de gestionnaire de ressources Azure sont des fichiers JavaScript Objet Notation (JSON) qui définissent l’environnement hello toobuild vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="42ef7-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="42ef7-197">modèles de Hello sont réparties dans les fournisseurs de ressources toodifferent tels que compute ou réseau.</span><span class="sxs-lookup"><span data-stu-id="42ef7-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="42ef7-198">Vous pouvez utiliser les modèles existants ou écrire les vôtres.</span><span class="sxs-lookup"><span data-stu-id="42ef7-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="42ef7-199">Découvrez plus d’informations sur [l’utilisation des modèles et de Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42ef7-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="42ef7-200">Au sein de hello `Microsoft.Compute/virtualMachines` fournisseur de votre modèle, vous avez un `storageProfile` nœud qui contient les détails de configuration hello pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="42ef7-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="42ef7-201">Hello deux principaux paramètres tooedit sont hello `image` et `vhd` URI qui pointent tooyour des disques personnalisées et disque virtuel de votre nouvelle VM.</span><span class="sxs-lookup"><span data-stu-id="42ef7-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="42ef7-202">suivant de Hello montre un exemple Hello JSON pour l’utilisation d’un disque personnalisé :</span><span class="sxs-lookup"><span data-stu-id="42ef7-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

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

<span data-ttu-id="42ef7-203">Vous pouvez utiliser [cette toocreate modèle existant une machine virtuelle à partir d’une image personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou consultez l’article sur [créer vos propres modèles Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="42ef7-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="42ef7-204">Une fois que vous avez un modèle configuré, utilisez [créer de déploiement de groupe az](/cli/azure/group/deployment#create) toocreate vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="42ef7-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="42ef7-205">Spécifiez hello URI de votre modèle de JSON avec hello `--template-uri` paramètre :</span><span class="sxs-lookup"><span data-stu-id="42ef7-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="42ef7-206">Si vous avez un fichier JSON stocké localement sur votre ordinateur, vous pouvez utiliser hello `--template-file` paramètre à la place :</span><span class="sxs-lookup"><span data-stu-id="42ef7-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="42ef7-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42ef7-207">Next steps</span></span>
<span data-ttu-id="42ef7-208">Après avoir préparé et chargé votre disque virtuel personnalisé, vous pouvez découvrir plus d’informations sur [l’utilisation de Resource Manager et des modèles](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42ef7-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="42ef7-209">Vous pouvez également trop[ajouter un disque de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="42ef7-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="42ef7-210">Si vous avez des applications en cours d’exécution sur vos ordinateurs virtuels que vous avez besoin de tooaccess, veillez trop[ouvrir les ports et les points de terminaison](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42ef7-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

