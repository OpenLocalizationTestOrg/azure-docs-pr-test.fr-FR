---
title: aaaUpdate votre appareil StorSimple | Documents Microsoft
description: "Explique comment toouse hello StorSimple mettre à jour tooinstall fonctionnalité régulière et des correctifs et mises à jour du mode de maintenance."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="8444e-103">Mettre à jour votre appareil StorSimple 8000 Series</span><span class="sxs-lookup"><span data-stu-id="8444e-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="8444e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8444e-104">Overview</span></span>
<span data-ttu-id="8444e-105">Hello StorSimple mises à jour les fonctionnalités permettent tooeasily jour votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8444e-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="8444e-106">Selon le type de mise à jour de hello, vous pouvez appliquer les appareil de toohello de mises à jour via le portail Azure classic de hello ou via l’interface Windows PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="8444e-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="8444e-107">Ce didacticiel décrit les types de mise à jour hello et comment tooinstall d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="8444e-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="8444e-108">Vous pouvez appliquer deux types de mises à jour d’appareil :</span><span class="sxs-lookup"><span data-stu-id="8444e-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="8444e-109">Mises à jour ordinaires (ou en mode Normal)</span><span class="sxs-lookup"><span data-stu-id="8444e-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="8444e-110">Mises à jour en mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="8444e-110">Maintenance mode updates</span></span>

<span data-ttu-id="8444e-111">Vous pouvez installer les mises à jour régulières via hello portail Azure classic ou Windows PowerShell ; Toutefois, vous devez utiliser des mises à jour du mode Maintenance tooinstall Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8444e-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="8444e-112">Chaque type de mise à jour est décrit séparément, ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8444e-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="8444e-113">Mises à jour ordinaires</span><span class="sxs-lookup"><span data-stu-id="8444e-113">Regular updates</span></span>
<span data-ttu-id="8444e-114">Mises à jour régulières sont mises à jour sans interruption de service qui peuvent être installés lors de l’appareil de hello est en mode Normal.</span><span class="sxs-lookup"><span data-stu-id="8444e-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="8444e-115">Ces mises à jour sont appliquées via le contrôleur de l’appareil tooeach du site Web Microsoft Update hello.</span><span class="sxs-lookup"><span data-stu-id="8444e-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8444e-116">Un basculement de contrôleur peut se produire pendant le processus de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="8444e-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="8444e-117">Mais cela n’aura aucune incidence sur la disponibilité ou le fonctionnement du système.</span><span class="sxs-lookup"><span data-stu-id="8444e-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="8444e-118">Pour plus d’informations sur comment tooinstall mises à jour régulières hello via le portail Azure classic, consultez [installer les mises à jour régulières via hello portail Azure classic](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="8444e-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="8444e-119">Vous pouvez également installer les mises à jour ordinaires via Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="8444e-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="8444e-120">Pour des informations détaillées, consultez la page [Installer les mises à jour ordinaires via Windows PowerShell pour StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="8444e-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="8444e-121">Mises à jour en mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="8444e-121">Maintenance mode updates</span></span>
<span data-ttu-id="8444e-122">Les mises à jour en mode Maintenance provoquent une interruption du service. Il s’agit, par exemple, des mises à niveau du microprogramme du disque.</span><span class="sxs-lookup"><span data-stu-id="8444e-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="8444e-123">Ces mises à jour nécessitent hello appareil toobe est placé en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8444e-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="8444e-124">Pour plus d’informations, consultez l’[Étape 2 : Passage en mode Maintenance](#step2).</span><span class="sxs-lookup"><span data-stu-id="8444e-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="8444e-125">Vous ne pouvez pas utiliser les mises à jour du mode Maintenance tooinstall de portail classique Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8444e-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="8444e-126">Vous devez utiliser Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8444e-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="8444e-127">Pour plus d’informations sur comment le mode de Maintenance tooinstall met à jour, consultez [mises à jour du mode de Maintenance d’installer via Windows PowerShell pour StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="8444e-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8444e-128">Mode de gestion des mises à jour doivent être appliquée séparément tooeach contrôleur.</span><span class="sxs-lookup"><span data-stu-id="8444e-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="8444e-129">Installer les mises à jour régulières via hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="8444e-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="8444e-130">Vous pouvez utiliser l’appareil StorSimple tooyour hello tooapply de portail classique Azure mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8444e-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="8444e-131">Installer les mises à jour ordinaires via Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="8444e-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="8444e-132">Ou bien, vous pouvez utiliser Windows PowerShell pour StorSimple tooapply les mises à jour régulières (mode Normal).</span><span class="sxs-lookup"><span data-stu-id="8444e-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8444e-133">Vous pouvez installer les mises à jour normales à l’aide de Windows PowerShell pour StorSimple, nous vous recommandons vivement d’installer les mises à jour régulières via hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="8444e-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="8444e-134">À partir de mise à jour 1, vérifications préalables sera effectuée tooinstalling préalable des mises à jour à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="8444e-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="8444e-135">Ces vérifications préalables permettent de prévenir les échecs et de garantir une expérience avec moins de problèmes.</span><span class="sxs-lookup"><span data-stu-id="8444e-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="8444e-136">Installer les mises à jour en mode Maintenance via Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="8444e-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="8444e-137">Vous utilisez Windows PowerShell pour l’appareil StorSimple de tooyour StorSimple tooapply Maintenance mode mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8444e-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="8444e-138">Dans ce mode, toutes les demandes d’E/S sont suspendues.</span><span class="sxs-lookup"><span data-stu-id="8444e-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="8444e-139">Services tels que de mémoire vive non volatile (NVRAM) ou le service de cluster de hello sont également arrêtés.</span><span class="sxs-lookup"><span data-stu-id="8444e-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="8444e-140">Les deux contrôleurs sont redémarrés lorsque vous entrez dans ce mode ou que vous le quittez.</span><span class="sxs-lookup"><span data-stu-id="8444e-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="8444e-141">Lorsque vous quittez ce mode, tous les services hello reprendront et doivent être sains.</span><span class="sxs-lookup"><span data-stu-id="8444e-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="8444e-142">(Cela peut prendre quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="8444e-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="8444e-143">Si vous avez besoin de mises à jour de mode de Maintenance tooapply, vous recevrez une alerte via hello portail classique Azure que vous disposez des mises à jour qui doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="8444e-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="8444e-144">Cette alerte inclut des instructions sur l’utilisation de Windows PowerShell pour les mises à jour de StorSimple tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="8444e-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="8444e-145">Une fois que vous mettez à jour votre appareil, utilisez hello même mode de procédure toochange hello périphérique tooRegular.</span><span class="sxs-lookup"><span data-stu-id="8444e-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="8444e-146">Pour obtenir des instructions détaillées, consultez l’ [Étape 4 : Sortie du mode Maintenance](#step4).</span><span class="sxs-lookup"><span data-stu-id="8444e-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="8444e-147">Avant de passer en mode Maintenance, vérifiez que les deux contrôleurs d’appareil sont intègres en vérifiant hello **état du matériel** sur hello **Maintenance** page Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="8444e-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="8444e-148">Si le contrôleur de hello n’est pas intègre, contactez le Support Microsoft pour les étapes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="8444e-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="8444e-149">Pour plus d’informations, consultez tooContact Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8444e-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="8444e-150">Lorsque vous êtes en mode Maintenance, vous devez tooapply hello tout d’abord les mises à jour sur un contrôleur et puis sur hello autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="8444e-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="8444e-151">Étape 1 : Connecter la console série de toohello<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="8444e-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="8444e-152">Tout d’abord, utilisez une application tel que PuTTY tooaccess hello console série.</span><span class="sxs-lookup"><span data-stu-id="8444e-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="8444e-153">Hello procédure suivante explique comment console série du toohello toouse tooconnect PuTTY.</span><span class="sxs-lookup"><span data-stu-id="8444e-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="8444e-154">Étape 2 : Passage en mode Maintenance <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="8444e-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="8444e-155">Une fois que vous vous connectez toohello console, déterminez s’il existe des mises à jour tooinstall et entrez tooinstall de mode de Maintenance les.</span><span class="sxs-lookup"><span data-stu-id="8444e-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="8444e-156">Étape 3 : Installation des mises à jour <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="8444e-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="8444e-157">Ensuite, installez les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8444e-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="8444e-158">Étape 4 : Sortie du mode Maintenance <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="8444e-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="8444e-159">Pour finir, quittez le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8444e-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="8444e-160">Installer les correctifs logiciels via Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="8444e-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="8444e-161">Contrairement aux mises à jour pour Microsoft Azure StorSimple, les correctifs logiciels sont installés à partir d’un dossier partagé.</span><span class="sxs-lookup"><span data-stu-id="8444e-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="8444e-162">Comme pour les mises à jour, il existe deux types de correctifs :</span><span class="sxs-lookup"><span data-stu-id="8444e-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="8444e-163">Correctifs logiciels ordinaires</span><span class="sxs-lookup"><span data-stu-id="8444e-163">Regular hotfixes</span></span> 
* <span data-ttu-id="8444e-164">Correctifs logiciels en mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="8444e-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="8444e-165">Hello procédures suivantes expliquent comment toouse Windows PowerShell pour tooinstall StorSimple régulière et des correctifs en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8444e-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="8444e-166">Que se passe-t-il tooupdates si vous effectuez une fabrique de réinitialisation du périphérique de hello ?</span><span class="sxs-lookup"><span data-stu-id="8444e-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="8444e-167">Si un appareil est toofactory de réinitialiser les paramètres, toutes les mises à jour de hello sont perdues.</span><span class="sxs-lookup"><span data-stu-id="8444e-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="8444e-168">Une fois l’appareil réinitialisé de hello est inscrit et configuré, vous devez toomanually installer les mises à jour via hello portail Azure classic et/ou de Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8444e-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="8444e-169">Pour plus d’informations sur les paramètres d’usine, consultez [rétablir les paramètres par défaut de hello appareil toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="8444e-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8444e-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8444e-170">Next steps</span></span>
* <span data-ttu-id="8444e-171">En savoir plus sur [à l’aide Windows PowerShell pour StorSimple tooadminister votre appareil StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8444e-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="8444e-172">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8444e-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

