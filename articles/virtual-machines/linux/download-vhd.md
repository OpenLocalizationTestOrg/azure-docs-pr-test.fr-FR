---
title: "aaaDownload un VHD Linux à partir de Azure | Documents Microsoft"
description: "Télécharger un VHD Linux à l’aide de hello CLI d’Azure et hello portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="c7f6a-103">Télécharger un disque VHD Linux à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="c7f6a-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="c7f6a-104">Dans cet article, vous apprendrez comment toodownload un [(VHD) du disque dur virtuel Linux](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) fichier à partir d’Azure à l’aide hello CLI d’Azure et le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="c7f6a-105">Machines virtuelles (VM) en cours d’utilisation Azure [disques](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) comme un toostore place un système d’exploitation, des applications et des données.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="c7f6a-106">Toutes les machines virtuelles Azure possèdent au moins deux disques : un disque de système d’exploitation Windows et un disque temporaire.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="c7f6a-107">disque de système d’exploitation Hello est initialement créé à partir d’une image et disque de système d’exploitation hello et image de hello sont des disques durs virtuels stockés dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="c7f6a-108">Les machines virtuelles peuvent également disposer d’un ou plusieurs disques de données, également stockés sur les VHD.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="c7f6a-109">Si ce n’est déjà fait, installez [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c7f6a-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="c7f6a-110">Arrêter hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c7f6a-110">Stop hello VM</span></span>

<span data-ttu-id="c7f6a-111">Un disque dur virtuel ne peut être téléchargé à partir d’Azure, si elle est attachée tooa machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="c7f6a-112">Vous devez toodownload de machine virtuelle hello toostop un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="c7f6a-113">Si vous voulez toouse un disque dur virtuel en tant qu’un [image](tutorial-custom-images.md) toocreate autres machines virtuelles avec de nouveaux disques, vous devez toodeprovision et généraliser le système d’exploitation de hello contenue dans hello de fichiers et d’arrêter hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="c7f6a-114">toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, vous seulement devez toostop et désallouer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="c7f6a-115">toouse hello de disque dur virtuel en tant qu’une image toocreate autres machines virtuelles, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c7f6a-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="c7f6a-116">Utiliser SSH, nom du compte hello et hello adresse IP publique de hello VM tooconnect tooit et annuler le déploiement.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="c7f6a-117">Bonjour + utilisateur paramètre supprime également le dernier compte d’utilisateur configuré hello.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="c7f6a-118">Si vous sont cuisson des informations d’identification de compte dans toohello VM, laissez cette + paramètre de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="c7f6a-119">Hello exemple suivant supprime hello dernier compte d’utilisateur configuré :</span><span class="sxs-lookup"><span data-stu-id="c7f6a-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="c7f6a-120">Se connecter tooyour compte Azure avec [ouverture de session az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c7f6a-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="c7f6a-121">Arrêter et désallouer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="c7f6a-122">Généraliser hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="c7f6a-123">toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c7f6a-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="c7f6a-124">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c7f6a-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="c7f6a-125">Dans le menu du Hub hello, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="c7f6a-126">Sélectionnez hello machine virtuelle à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="c7f6a-127">Dans le panneau hello pour hello machine virtuelle, cliquez sur **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![Arrêter la machine virtuelle](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="c7f6a-129">Générer une URL de SAP</span><span class="sxs-lookup"><span data-stu-id="c7f6a-129">Generate SAS URL</span></span>

<span data-ttu-id="c7f6a-130">fichier de disque dur virtuel toodownload hello, vous devez toogenerate une [signature d’accès partagé (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="c7f6a-131">Lorsque l’URL de hello est généré, un délai d’expiration est affecté toohello URL.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="c7f6a-132">Dans menu hello du panneau hello pour hello machine virtuelle, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="c7f6a-133">Sélectionnez le disque du système d’exploitation hello pour hello machine virtuelle, puis cliquez sur **exporter**.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="c7f6a-134">Cliquez sur **Générer l’URL**.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-134">Click **Generate URL**.</span></span>

    ![Générer une URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="c7f6a-136">Télécharger un VHD</span><span class="sxs-lookup"><span data-stu-id="c7f6a-136">Download VHD</span></span>

1.  <span data-ttu-id="c7f6a-137">URL hello qui a été généré, cliquez sur fichier de disque dur virtuel de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Télécharger un VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="c7f6a-139">Vous devrez peut-être tooclick **enregistrer** dans le téléchargement de hello navigateur toostart hello.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="c7f6a-140">nom par défaut de Hello pour le fichier de disque dur virtuel hello est *abcd*.</span><span class="sxs-lookup"><span data-stu-id="c7f6a-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Cliquez sur Enregistrer dans le navigateur de hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="c7f6a-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7f6a-142">Next steps</span></span>

- <span data-ttu-id="c7f6a-143">Découvrez comment trop[télécharger et de créer un VM Linux à partir du disque personnalisé avec hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c7f6a-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="c7f6a-144">[Gérer les disques Azure hello CLI d’Azure](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c7f6a-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

