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
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="9f7fb-103">Créer une VM Linux à partir du disque personnalisé avec hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9f7fb-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="9f7fb-104">Cet article vous explique comment tooupload un disque dur virtuel (VHD) personnalisé ou copier un un disque dur virtuel existant dans Azure et créer de nouveaux Linux ordinateurs virtuels (VM) à partir du disque de personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="9f7fb-105">Vous pouvez installer et configurer les exigences de tooyour distribution de Linux et ensuite utiliser ce disque dur virtuel tooquickly créer une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="9f7fb-106">Si vous souhaitez toocreate plusieurs machines virtuelles à partir de votre disque personnalisée, vous devez créer une image à partir de votre machine virtuelle ou un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="9f7fb-107">Pour plus d’informations, consultez [créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="9f7fb-108">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-108">You have two options:</span></span>
* [<span data-ttu-id="9f7fb-109">Charger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="9f7fb-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="9f7fb-110">Copier une machine virtuelle Azure existante</span><span class="sxs-lookup"><span data-stu-id="9f7fb-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="9f7fb-111">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="9f7fb-111">Quick commands</span></span>

<span data-ttu-id="9f7fb-112">Lorsque vous créez une nouvelle machine virtuelle en utilisant [az vm créer](/cli/azure/vm#create) à partir d’un disque spécialisé ou personnalisé vous **attacher** disque de hello (--attacher de disque de système d’exploitation) au lieu de spécifier une image personnalisée ou marketplace (--image).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="9f7fb-113">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* à l’aide de hello gérés disque nommé *myManagedDisk* créé à partir de votre disque dur virtuel personnalisé :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="9f7fb-114">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="9f7fb-114">Requirements</span></span>
<span data-ttu-id="9f7fb-115">toocomplete hello comme suit, vous devez :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="9f7fb-116">Une machine virtuelle Linux qui a été préparée pour une utilisation dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="9f7fb-117">Hello [Prepare hello VM](#prepare-the-vm) section de cet article décrit comment toofind distribution des informations spécifiques sur l’installation de hello Linux Agent Azure (waagent) qui est requis pour toowork de machine virtuelle hello correctement dans Azure et pour vous tooconnect en mesure de toobe tooit à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="9f7fb-118">fichier de disque dur virtuel Hello d’un existant [distribution Linux d’approuvées Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consultez [plus d’informations pour les distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa de disque virtuel au format de disque dur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="9f7fb-119">Plusieurs outils existent toocreate une machine virtuelle et le disque dur virtuel :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="9f7fb-120">Installer et configurer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), en prenant soin de toouse disque dur virtuel en tant que format de votre image.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="9f7fb-121">Vous pouvez [convertir une image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) à l’aide de la commande **qemu-img convert** si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="9f7fb-122">Vous pouvez également utiliser Hyper-V [sur Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [sur Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="9f7fb-123">nouveau format VHDX de Hello n’est pas pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="9f7fb-124">Lorsque vous créez une machine virtuelle, spécifiez le disque dur virtuel en tant que format de hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="9f7fb-125">Si nécessaire, vous pouvez convertir à l’aide de tooVHD de disques VHDX [qemu-img convertir](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="9f7fb-126">En outre, Azure ne prend pas en charge téléchargement de disques durs virtuels dynamiques, par conséquent, vous devez tooconvert ce toostatic disques vhd avant de télécharger.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="9f7fb-127">Vous pouvez utiliser des outils tels que [utilitaires de disque dur virtuel de Azure pour atteindre](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert les disques dynamiques pendant le processus hello de téléchargement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="9f7fb-128">Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="9f7fb-129">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9f7fb-130">Les noms de paramètre sont par exemple *myResourceGroup*, *mystorageaccount* et *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="9f7fb-131"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="9f7fb-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="9f7fb-132">Préparer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9f7fb-132">Prepare hello VM</span></span>

<span data-ttu-id="9f7fb-133">Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="9f7fb-134">Hello suivant articles vous guide tout au long de la tooprepare hello diverses distributions Linux prises en charge sur Azure :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="9f7fb-135">Distributions CentOS</span><span class="sxs-lookup"><span data-stu-id="9f7fb-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9f7fb-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="9f7fb-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9f7fb-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="9f7fb-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9f7fb-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="9f7fb-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9f7fb-139">SLES et openSUSE</span><span class="sxs-lookup"><span data-stu-id="9f7fb-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9f7fb-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9f7fb-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9f7fb-141">Autres - Distributions non approuvées</span><span class="sxs-lookup"><span data-stu-id="9f7fb-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="9f7fb-142">Voir aussi hello [Notes d’Installation Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir des conseils plus générales sur la préparation d’images Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="9f7fb-143">Hello [la plateforme Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applique tooVMs Linux en cours d’exécution lorsque un des hello visé distributions est utilisé uniquement avec les détails de configuration hello comme indiqué dans la section « Prise en charge des Versions » en [Linux sur Azure approuvées Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="9f7fb-144">Option 1 : charger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="9f7fb-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="9f7fb-145">Vous pouvez charger un disque dur virtuel personnalisé s’exécutant sur un ordinateur local ou que vous avez exporté à partir d’un autre cloud.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="9f7fb-146">toocreate de disque dur virtuel hello toouse une machine virtuelle Azure, vous devez stockage tooa de tooupload hello VHD compte et créez un disque géré à partir de hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="9f7fb-147">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="9f7fb-147">Create a resource group</span></span>

<span data-ttu-id="9f7fb-148">Avant de télécharger de votre disque personnalisée et création de machines virtuelles, vous devez toocreate un groupe de ressources avec [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="9f7fb-149">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement : [vue d’ensemble de disques gérés d’Azure](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9f7fb-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="9f7fb-150">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-150">Create a storage account</span></span>

<span data-ttu-id="9f7fb-151">Créez un compte de stockage pour votre disque personnalisé et vos machines virtuelles avec la commande [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="9f7fb-152">Hello exemple suivant crée un compte de stockage nommé *mystorageaccount* dans le groupe de ressources hello créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="9f7fb-153">Répertorier les clés de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="9f7fb-153">List storage account keys</span></span>
<span data-ttu-id="9f7fb-154">Azure génère deux clés d’accès de 512 bits pour chaque compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="9f7fb-155">Ces clés d’accès sont utilisées lors de l’authentification de compte de stockage toohello, comme effectuer des opérations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="9f7fb-156">En savoir plus sur [la gestion des accès toostorage ici](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="9f7fb-157">Vous permet d’afficher les clés d’accès hello avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="9f7fb-158">Afficher les touches d’accès hello pour le compte de stockage hello créé :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="9f7fb-159">résultat de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="9f7fb-160">Prenez note de **key1** comme vous l’utiliserez toointeract avec votre compte de stockage dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="9f7fb-161">Créer un conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="9f7fb-161">Create a storage container</span></span>
<span data-ttu-id="9f7fb-162">Bonjour même façon que vous créez des répertoires différents toologically organiser votre système de fichiers local, vous créez des conteneurs au sein d’un tooorganize de compte de stockage vos disques.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="9f7fb-163">Un compte de stockage peut contenir un certain nombre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="9f7fb-164">Créez un conteneur avec la commande [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="9f7fb-165">Hello exemple suivant crée un conteneur nommé *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="9f7fb-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="9f7fb-166">Télécharger hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="9f7fb-166">Upload hello VHD</span></span>
<span data-ttu-id="9f7fb-167">Chargez votre disque personnalisé avec la commande [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="9f7fb-168">Téléchargez et stockez votre disque personnalisé en tant qu’objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="9f7fb-169">Spécifiez votre clé d’accès, le conteneur hello créé à l’étape précédente de hello, puis hello disque personnalisé de chemin d’accès toohello sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="9f7fb-170">Téléchargement hello de disque dur virtuel peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="9f7fb-171">Créer un disque géré</span><span class="sxs-lookup"><span data-stu-id="9f7fb-171">Create a managed disk</span></span>


<span data-ttu-id="9f7fb-172">Créer un disque géré à partir de l’aide de disque dur virtuel hello [az créer](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="9f7fb-173">Hello exemple suivant crée un disque géré nommé *myManagedDisk* de hello disque dur virtuel, vous avez téléchargé tooyour compte de stockage et de conteneur :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="9f7fb-174">Option 2 : copier une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="9f7fb-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="9f7fb-175">Vous pouvez également créer hello personnalisé de machine virtuelle dans Azure, puis copier une disquette hello du système d’exploitation et l’attacher tooa nouvelle machine virtuelle toocreate une autre copie.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="9f7fb-176">Cela convient pour le test, mais si vous souhaitez toouse une machine virtuelle Azure existante comme modèle de hello pour plusieurs nouveaux ordinateurs virtuels, vous devez vraiment créer un **image** à la place.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="9f7fb-177">Pour plus d’informations sur la création d’une image à partir d’une machine virtuelle Azure existante, consultez [créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="9f7fb-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="9f7fb-178">Créer un instantané</span><span class="sxs-lookup"><span data-stu-id="9f7fb-178">Create a snapshot</span></span>

<span data-ttu-id="9f7fb-179">Cet exemple crée l’instantané d’une machine virtuelle nommée *myVM* dans le groupe de ressources *myResourceGroup* et crée un instantané nommé *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="9f7fb-180">Créer le disque géré de hello</span><span class="sxs-lookup"><span data-stu-id="9f7fb-180">Create hello managed disk</span></span>

<span data-ttu-id="9f7fb-181">Créer un nouveau disque géré à partir de l’instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="9f7fb-182">Obtenir l’ID de hello d’instantané de hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="9f7fb-183">Dans cet exemple, l’instantané d’hello est nommé *osDiskSnapshot* et se trouve dans hello *myResourceGroup* groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="9f7fb-184">Créer un disque géré de hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-184">Create hello managed disk.</span></span> <span data-ttu-id="9f7fb-185">Dans cet exemple, nous allons créer un disque géré nommé *myManagedDisk* à partir de notre instantané, qui représente 128 Go de stockage standard.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="9f7fb-186">Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9f7fb-186">Create hello VM</span></span>

<span data-ttu-id="9f7fb-187">Maintenant, créez votre machine virtuelle avec [az vm créer](/cli/azure/vm#create) et d’attachement (--attacher de disque de système d’exploitation) hello gérés disque comme disque de hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="9f7fb-188">Hello exemple suivant crée un ordinateur virtuel nommé *myNewVM* à l’aide de hello gérés disque créé à partir de votre disque dur virtuel chargé :</span><span class="sxs-lookup"><span data-stu-id="9f7fb-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="9f7fb-189">Vous devez être en mesure de tooSSH dans hello machine virtuelle à l’aide des informations d’identification hello à partir de l’ordinateur virtuel source de hello.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9f7fb-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f7fb-190">Next steps</span></span>
<span data-ttu-id="9f7fb-191">Après avoir préparé et chargé votre disque virtuel personnalisé, vous pouvez découvrir plus d’informations sur [l’utilisation de Resource Manager et des modèles](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="9f7fb-192">Vous pouvez également trop[ajouter un disque de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9f7fb-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="9f7fb-193">Si vous avez des applications en cours d’exécution sur vos ordinateurs virtuels que vous avez besoin de tooaccess, veillez trop[ouvrir les ports et les points de terminaison](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f7fb-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

