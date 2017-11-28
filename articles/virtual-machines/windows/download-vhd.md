---
title: "Télécharger un VHD Windows à partir d’Azure | Microsoft Docs"
description: "Téléchargez un VHD Windows à l’aide du Portail Azure."
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
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="321b2-103">Télécharger un VHD Windows à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="321b2-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="321b2-104">Dans cet article, vous apprendrez à télécharger un fichier de [disque dur virtuel (VHD) Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à partir d’Azure à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="321b2-104">In this article, you learn how to download a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using the Azure portal.</span></span> 

<span data-ttu-id="321b2-105">Les machines virtuelles dans Azure utilisent des [disques](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) comme emplacement de stockage d’un système d’exploitation, d’applications et de données.</span><span class="sxs-lookup"><span data-stu-id="321b2-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="321b2-106">Toutes les machines virtuelles Azure possèdent au moins deux disques : un disque de système d’exploitation Windows et un disque temporaire.</span><span class="sxs-lookup"><span data-stu-id="321b2-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="321b2-107">Le disque de système d’exploitation est initialement créé à partir d’une image. Tant le disque que l’image sont des disques VHD stockés dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="321b2-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="321b2-108">Les machines virtuelles peuvent également disposer d’un ou plusieurs disques de données, également stockés sur les VHD.</span><span class="sxs-lookup"><span data-stu-id="321b2-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="321b2-109">Arrêtez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="321b2-109">Stop the VM</span></span>

<span data-ttu-id="321b2-110">Il n’est pas possible de télécharger un disque VHD associé à une machine virtuelle en cours d’exécution à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="321b2-110">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="321b2-111">Il vous faut arrêter la machine virtuelle pour télécharger un VHD.</span><span class="sxs-lookup"><span data-stu-id="321b2-111">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="321b2-112">Si vous souhaitez utiliser un VHD en tant [qu’image](tutorial-custom-images.md) afin de créer d’autres machines virtuelles avec de nouveaux disques, utilisez [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) pour généraliser le système d’exploitation contenu dans le fichier, puis arrêtez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="321b2-112">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) to generalize the operating system contained in the file and then stop the VM.</span></span> <span data-ttu-id="321b2-113">Pour utiliser le VHD en tant que disque d’une nouvelle instance d’une machine virtuelle ou d’un disque de données existant, il vous suffit d’arrêter et de libérer de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="321b2-113">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="321b2-114">Pour utiliser le VHD en tant qu’image pour créer d’autres machines virtuelles, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="321b2-114">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="321b2-115">Si ce n’est pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="321b2-115">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="321b2-116">[Connectez-vous à la machine virtuelle](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="321b2-116">[Connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="321b2-117">Sur la machine virtuelle, ouvrez la fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="321b2-117">On the VM, open the Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="321b2-118">Remplacez le répertoire par *%windir%\system32\sysprep* et exécutez sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="321b2-118">Change the directory to *%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="321b2-119">Dans la boîte de dialogue Outil de préparation du système, sélectionnez **Entrer en mode OOBE (Out-of-Box Experience) du système** et vérifiez que **Généraliser** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="321b2-119">In the System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="321b2-120">Dans Options d’arrêt, sélectionnez **Arrêter**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="321b2-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="321b2-121">Pour utiliser le VHD en tant que disque d’une nouvelle instance d’une machine virtuelle ou d’un disque de données existant, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="321b2-121">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="321b2-122">Dans le menu Hub du Portail Azure, cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="321b2-122">On the Hub menu in the Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="321b2-123">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="321b2-123">Select the VM from the list.</span></span>
3.  <span data-ttu-id="321b2-124">Dans le panneau de la machine virtuelle, cliquez sur **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="321b2-124">On the blade for the VM, click **Stop**.</span></span>

    ![Arrêter la machine virtuelle](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="321b2-126">Générer une URL de SAP</span><span class="sxs-lookup"><span data-stu-id="321b2-126">Generate SAS URL</span></span>

<span data-ttu-id="321b2-127">Pour télécharger le fichier VHD, vous devez générer une URL de [signature d’accès partagé (SAP)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="321b2-127">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="321b2-128">Un délai d’expiration est affecté à l’URL lors de sa génération.</span><span class="sxs-lookup"><span data-stu-id="321b2-128">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="321b2-129">Dans le menu du panneau de la machine virtuelle, cliquez sur **Disques**.</span><span class="sxs-lookup"><span data-stu-id="321b2-129">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="321b2-130">Sélectionnez le disque de système d’exploitation de la machine virtuelle, puis cliquez sur **Exporter**.</span><span class="sxs-lookup"><span data-stu-id="321b2-130">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="321b2-131">Fixez le délai d’expiration de l’URL sur *36000*.</span><span class="sxs-lookup"><span data-stu-id="321b2-131">Set the expiration time of the URL to *36000*.</span></span>
4.  <span data-ttu-id="321b2-132">Cliquez sur **Générer l’URL**.</span><span class="sxs-lookup"><span data-stu-id="321b2-132">Click **Generate URL**.</span></span>

    ![Générer une URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="321b2-134">Le délai d’expiration est augmenté par rapport à la valeur par défaut afin de laisser suffisamment de temps pour télécharger le fichier volumineux de VHD pour un système d’exploitation Windows Server.</span><span class="sxs-lookup"><span data-stu-id="321b2-134">The expiration time is increased from the default to provide enough time to download the large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="321b2-135">En général, le téléchargement d’un fichier de VHD contenant le système d’exploitation Windows prend plusieurs heures, en fonction de la connexion.</span><span class="sxs-lookup"><span data-stu-id="321b2-135">You can expect a VHD file that contains the Windows Server operating system to take several hours to download depending on your connection.</span></span> <span data-ttu-id="321b2-136">Si vous téléchargez un VHD pour un disque de données, le délai par défaut est suffisant.</span><span class="sxs-lookup"><span data-stu-id="321b2-136">If you are downloading a VHD for a data disk, the default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="321b2-137">Télécharger un VHD</span><span class="sxs-lookup"><span data-stu-id="321b2-137">Download VHD</span></span>

1.  <span data-ttu-id="321b2-138">Sous l’URL générée, cliquez sur Télécharger le fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="321b2-138">Under the URL that was generated, click Download the VHD file.</span></span>

    ![Télécharger un VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="321b2-140">Vous devrez peut-être cliquer sur **Enregistrer** dans le navigateur pour commencer le téléchargement.</span><span class="sxs-lookup"><span data-stu-id="321b2-140">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="321b2-141">Le nom par défaut du fichier VHD est *abcd*.</span><span class="sxs-lookup"><span data-stu-id="321b2-141">The default name for the VHD file is *abcd*.</span></span>

    ![Cliquez sur Enregistrer dans le navigateur](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="321b2-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="321b2-143">Next steps</span></span>

- <span data-ttu-id="321b2-144">Découvrez comment [charger un fichier de VHD sur Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="321b2-144">Learn how to [upload a VHD file to Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="321b2-145">[Créez des disques gérés à partir de disques non gérés dans un compte de stockage](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="321b2-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="321b2-146">[Gérez des disques Azure avec PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="321b2-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

