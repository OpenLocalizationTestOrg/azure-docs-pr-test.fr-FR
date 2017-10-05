---
title: "Capture d’une image de machine virtuelle Microsoft Azure | Microsoft Docs"
description: "Capturer l’image d’une machine virtuelle Microsoft Azure créée avec le modèle de déploiement classique"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 6032263848c469ce2f416306e5c91c29f4cb30e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="fc31a-103">Capturer l’image d’une machine virtuelle Microsoft Azure créée avec le modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="fc31a-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc31a-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fc31a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc31a-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="fc31a-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="fc31a-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc31a-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fc31a-107">Pour plus d’informations sur le modèle Azure Resource Manager, voir [Capturer une image managée d’une machine virtuelle généralisée dans Azure](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="fc31a-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="fc31a-108">Cet article vous montre comment capturer une machine virtuelle Azure exécutant Windows de façon à l’utiliser comme image pour créer d’autres machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="fc31a-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="fc31a-109">Cette image contient le disque du système d’exploitation et les disques de données éventuellement associés à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fc31a-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="fc31a-110">Comme elle ne comporte pas de configurations de mise en réseau, vous devrez établir des configurations réseau quand vous créez les autres machines virtuelles à partir de l’image.</span><span class="sxs-lookup"><span data-stu-id="fc31a-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="fc31a-111">Azure stocke l’image sous **Images de machine virtuelle (classic)**, un service **Compute** répertorié lorsque vous affichez tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="fc31a-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="fc31a-112">Il s’agit de l’emplacement où sont stockées les images que vous avez éventuellement téléchargées.</span><span class="sxs-lookup"><span data-stu-id="fc31a-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="fc31a-113">Pour plus d’informations sur les images, consultez la page [À propos des images pour les machines virtuelles](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc31a-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fc31a-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="fc31a-114">Before you begin</span></span>
<span data-ttu-id="fc31a-115">Ces étapes partent du principe que vous avez déjà créé une machine virtuelle Azure, configuré le système d’exploitation et attaché les disques de données.</span><span class="sxs-lookup"><span data-stu-id="fc31a-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="fc31a-116">Si vous ne l’avez pas encore fait, consultez les articles suivants pour obtenir plus d’informations sur la création et la préparation de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="fc31a-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="fc31a-117">Création d’une machine virtuelle à partir d’une image</span><span class="sxs-lookup"><span data-stu-id="fc31a-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="fc31a-118">Comment attacher un disque de données à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fc31a-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="fc31a-119">Assurez-vous que les rôles serveur sont pris en charge avec Sysprep.</span><span class="sxs-lookup"><span data-stu-id="fc31a-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="fc31a-120">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="fc31a-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="fc31a-121">Ce processus supprime la machine virtuelle d’origine une fois celle-ci capturée.</span><span class="sxs-lookup"><span data-stu-id="fc31a-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="fc31a-122">Avant de capturer une image d’une machine virtuelle Azure, nous vous recommandons de sauvegarder la machine virtuelle cible.</span><span class="sxs-lookup"><span data-stu-id="fc31a-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="fc31a-123">Les machines virtuelles Azure peuvent être sauvegardées à l’aide d’Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="fc31a-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="fc31a-124">Pour plus d’informations, voir [Sauvegarde des machines virtuelles Azure](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="fc31a-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="fc31a-125">D’autres solutions sont disponibles auprès de partenaires certifiés.</span><span class="sxs-lookup"><span data-stu-id="fc31a-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="fc31a-126">Pour savoir ce qui est actuellement disponible, faites une recherche dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fc31a-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="fc31a-127">Capture de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fc31a-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="fc31a-128">Dans le [portail Azure](http://portal.azure.com), **connectez-vous** à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fc31a-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="fc31a-129">Pour obtenir des instructions, consultez la rubrique [Comment se connecter à une machine virtuelle exécutant Windows Server][How to sign in to a virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="fc31a-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="fc31a-130">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fc31a-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="fc31a-131">Accédez au répertoire `%windir%\system32\sysprep`, puis exécutez sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="fc31a-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="fc31a-132">La boîte de dialogue **Outil de préparation système** apparaît.</span><span class="sxs-lookup"><span data-stu-id="fc31a-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="fc31a-133">Effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc31a-133">Do the following:</span></span>

   * <span data-ttu-id="fc31a-134">Dans **Action de nettoyage du système**, sélectionnez **Entrer en mode OOBE (OOBE)** et vérifiez que la case à cocher **Généraliser** est activée.</span><span class="sxs-lookup"><span data-stu-id="fc31a-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="fc31a-135">Pour plus d’informations sur l’utilisation de Sysprep, consultez la page [Introduction à l’utilisation de Sysprep][How to Use Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="fc31a-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="fc31a-136">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="fc31a-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="fc31a-137">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc31a-137">Click **OK**.</span></span>

   ![Exécutez Sysprep](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="fc31a-139">Sysprep arrête la machine virtuelle, ce qui a pour effet de modifier l’état de celle-ci en **Arrêté**dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fc31a-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure portal to **Stopped**.</span></span>
6. <span data-ttu-id="fc31a-140">Dans le portail Azure, cliquez sur **Machines virtuelles (classic)**, puis sélectionnez la machine virtuelle à capturer.</span><span class="sxs-lookup"><span data-stu-id="fc31a-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="fc31a-141">Le groupe **Images de machine virtuelle (classic)** est répertorié sous **Compute** lorsque vous affichez **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="fc31a-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="fc31a-142">Dans la barre de commandes, cliquez sur **Capture**.</span><span class="sxs-lookup"><span data-stu-id="fc31a-142">On the command bar, click **Capture**.</span></span>

   ![Capture machine virtuelle](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="fc31a-144">La boîte de dialogue **Capture the Virtual Machine** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fc31a-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="fc31a-145">Dans **Image Name**, entrez le nom de la nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="fc31a-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="fc31a-146">Dans **Image label**, tapez une étiquette pour la nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="fc31a-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="fc31a-147">Cliquez sur **J’ai exécuté Sysprep sur la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="fc31a-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="fc31a-148">Cette case à cocher fait référence aux actions avec Sysprep dans les étapes 3 à 5.</span><span class="sxs-lookup"><span data-stu-id="fc31a-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="fc31a-149">Une image _doit_ être généralisée en exécutant Sysprep avant d’ajouter une image Windows Server à votre jeu d’images personnalisées.</span><span class="sxs-lookup"><span data-stu-id="fc31a-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="fc31a-150">Une fois la capture terminée, la nouvelle image est disponible dans **Place de marché**, dans le conteneur **Compute**, **Images de machine virtuelle (classic)**.</span><span class="sxs-lookup"><span data-stu-id="fc31a-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![Capture d’image réussie](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="fc31a-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc31a-152">Next steps</span></span>
<span data-ttu-id="fc31a-153">L’image est prête à être utilisée pour créer des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="fc31a-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="fc31a-154">Pour ce faire, vous allez créer une machine virtuelle en sélectionnant l’élément de menu **Plus de services** en bas du menu Services, puis **Images de machine virtuelle (classic)** dans le groupe **Compute**.</span><span class="sxs-lookup"><span data-stu-id="fc31a-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="fc31a-155">Pour obtenir des instructions, consultez [Création d’une machine virtuelle à partir d’une image](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="fc31a-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/capture-image/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
