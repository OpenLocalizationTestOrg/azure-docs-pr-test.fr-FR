---
title: "aaaDownload un disque dur virtuel Windows à partir de Azure | Documents Microsoft"
description: "Téléchargez un disque dur virtuel Windows à l’aide de hello portail Azure."
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="15ac7-103">Télécharger un VHD Windows à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="15ac7-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="15ac7-104">Dans cet article, vous apprendrez comment toodownload un [(VHD) du disque dur virtuel Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fichier à partir d’Azure à l’aide hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15ac7-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="15ac7-105">Machines virtuelles (VM) en cours d’utilisation Azure [disques](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) comme un toostore place un système d’exploitation, des applications et des données.</span><span class="sxs-lookup"><span data-stu-id="15ac7-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="15ac7-106">Toutes les machines virtuelles Azure possèdent au moins deux disques : un disque de système d’exploitation Windows et un disque temporaire.</span><span class="sxs-lookup"><span data-stu-id="15ac7-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="15ac7-107">disque de système d’exploitation Hello est initialement créé à partir d’une image et disque de système d’exploitation hello et image de hello sont des disques durs virtuels stockés dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="15ac7-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="15ac7-108">Les machines virtuelles peuvent également disposer d’un ou plusieurs disques de données, également stockés sur les VHD.</span><span class="sxs-lookup"><span data-stu-id="15ac7-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="15ac7-109">Arrêter hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="15ac7-109">Stop hello VM</span></span>

<span data-ttu-id="15ac7-110">Un disque dur virtuel ne peut être téléchargé à partir d’Azure, si elle est attachée tooa machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="15ac7-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="15ac7-111">Vous devez toodownload de machine virtuelle hello toostop un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="15ac7-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="15ac7-112">Si vous voulez toouse un disque dur virtuel en tant qu’un [image](tutorial-custom-images.md) toocreate autres machines virtuelles avec de nouveaux disques, vous utilisez [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello du système d’exploitation contenu dans le fichier de hello et arrêtez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="15ac7-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="15ac7-113">toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, vous seulement devez toostop et désallouer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15ac7-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="15ac7-114">toouse hello de disque dur virtuel en tant qu’une image toocreate autres machines virtuelles, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="15ac7-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="15ac7-115">Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="15ac7-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="15ac7-116">[Se connecter toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15ac7-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="15ac7-117">Sur la machine virtuelle de hello, ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="15ac7-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="15ac7-118">Basculez hello trop*%windir%\system32\sysprep* et exécutez sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="15ac7-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="15ac7-119">Dans la boîte de dialogue Outil de préparation système hello, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et vous assurer que **Generalize** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="15ac7-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="15ac7-120">Dans Options d’arrêt, sélectionnez **Arrêter**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="15ac7-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="15ac7-121">toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="15ac7-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="15ac7-122">Dans menu Hub hello hello portail Azure, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="15ac7-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="15ac7-123">Sélectionnez hello machine virtuelle à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="15ac7-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="15ac7-124">Dans le panneau hello pour hello machine virtuelle, cliquez sur **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="15ac7-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![Arrêter la machine virtuelle](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="15ac7-126">Générer une URL de SAP</span><span class="sxs-lookup"><span data-stu-id="15ac7-126">Generate SAS URL</span></span>

<span data-ttu-id="15ac7-127">fichier de disque dur virtuel toodownload hello, vous devez toogenerate une [signature d’accès partagé (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="15ac7-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="15ac7-128">Lorsque l’URL de hello est généré, un délai d’expiration est affecté toohello URL.</span><span class="sxs-lookup"><span data-stu-id="15ac7-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="15ac7-129">Dans menu hello du panneau hello pour hello machine virtuelle, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="15ac7-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="15ac7-130">Sélectionnez le disque du système d’exploitation hello pour hello machine virtuelle, puis cliquez sur **exporter**.</span><span class="sxs-lookup"><span data-stu-id="15ac7-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="15ac7-131">Définir le délai d’expiration de hello de hello URL trop*36000*.</span><span class="sxs-lookup"><span data-stu-id="15ac7-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="15ac7-132">Cliquez sur **Générer l’URL**.</span><span class="sxs-lookup"><span data-stu-id="15ac7-132">Click **Generate URL**.</span></span>

    ![Générer une URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="15ac7-134">délai d’expiration de Hello est augmentée de hello par défaut tooprovide suffisamment de temps toodownload hello grand fichier de disque dur virtuel pour un système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="15ac7-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="15ac7-135">Vous pouvez vous attendre un fichier de disque dur virtuel qui contient tootake de système d’exploitation Windows Server hello plusieurs toodownload heures en fonction de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="15ac7-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="15ac7-136">Si vous téléchargez un disque dur virtuel pour un disque de données, la durée par défaut de hello est suffisante.</span><span class="sxs-lookup"><span data-stu-id="15ac7-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="15ac7-137">Télécharger un VHD</span><span class="sxs-lookup"><span data-stu-id="15ac7-137">Download VHD</span></span>

1.  <span data-ttu-id="15ac7-138">URL hello qui a été généré, cliquez sur fichier de disque dur virtuel de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="15ac7-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Télécharger un VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="15ac7-140">Vous devrez peut-être tooclick **enregistrer** dans le téléchargement de hello navigateur toostart hello.</span><span class="sxs-lookup"><span data-stu-id="15ac7-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="15ac7-141">nom par défaut de Hello pour le fichier de disque dur virtuel hello est *abcd*.</span><span class="sxs-lookup"><span data-stu-id="15ac7-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Cliquez sur Enregistrer dans le navigateur de hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="15ac7-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15ac7-143">Next steps</span></span>

- <span data-ttu-id="15ac7-144">Découvrez comment trop[télécharger un tooAzure de fichier de disque dur virtuel](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15ac7-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="15ac7-145">[Créez des disques gérés à partir de disques non gérés dans un compte de stockage](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15ac7-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="15ac7-146">[Gérez des disques Azure avec PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15ac7-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

