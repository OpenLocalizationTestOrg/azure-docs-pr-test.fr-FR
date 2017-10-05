---
title: "Changer le mode de l’appareil StorSimple | Microsoft Docs"
description: "Décrit les modes de l’appareil StorSimple et explique comment utiliser Windows PowerShell for StorSimple pour changer le mode de l’appareil."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: dd160ede1189b0de544c8cf5db3b13228d212419
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="ba55d-103">Changement du mode de votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="ba55d-103">Change the device mode on your StorSimple device</span></span>

<span data-ttu-id="ba55d-104">Cet article fournit une brève description des modes avec lesquels votre appareil StorSimple peut fonctionner.</span><span class="sxs-lookup"><span data-stu-id="ba55d-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="ba55d-105">Votre appareil StorSimple peut fonctionner dans trois modes : Normal, Maintenance et Récupération.</span><span class="sxs-lookup"><span data-stu-id="ba55d-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="ba55d-106">À la fin de cet article, vous :</span><span class="sxs-lookup"><span data-stu-id="ba55d-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="ba55d-107">Description des modes de l'appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="ba55d-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="ba55d-108">Comment déterminer le mode dans lequel se trouve l'appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="ba55d-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="ba55d-109">Comment passer du mode Normal au mode Maintenance, et *inversement*</span><span class="sxs-lookup"><span data-stu-id="ba55d-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="ba55d-110">Les tâches de gestion ci-dessus peuvent uniquement être effectuées via l’interface Windows PowerShell de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ba55d-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="ba55d-111">À propos des modes de l’appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="ba55d-111">About StorSimple device modes</span></span>

<span data-ttu-id="ba55d-112">Votre appareil StorSimple peut fonctionner en mode Normal, Maintenance ou Récupération.</span><span class="sxs-lookup"><span data-stu-id="ba55d-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="ba55d-113">Chacun de ces modes est brièvement décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ba55d-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="ba55d-114">Mode Normal</span><span class="sxs-lookup"><span data-stu-id="ba55d-114">Normal mode</span></span>

<span data-ttu-id="ba55d-115">Il s’agit du mode de fonctionnement normal pour un appareil StorSimple entièrement configuré.</span><span class="sxs-lookup"><span data-stu-id="ba55d-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="ba55d-116">Par défaut, votre appareil doit être en mode Normal.</span><span class="sxs-lookup"><span data-stu-id="ba55d-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="ba55d-117">Mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="ba55d-117">Maintenance mode</span></span>

<span data-ttu-id="ba55d-118">Parfois, l’appareil StorSimple doit être mis en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ba55d-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="ba55d-119">Ce mode vous permet d’assurer la maintenance de l’appareil et d’installer des mises à jour perturbatrices, telles que celles du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="ba55d-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="ba55d-120">Vous ne pouvez mettre le système en mode Maintenance qu’à l’aide de Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ba55d-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="ba55d-121">Dans ce mode, toutes les demandes d’E/S sont suspendues.</span><span class="sxs-lookup"><span data-stu-id="ba55d-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="ba55d-122">Les services tels que la mémoire vive non volatile (NVRAM) ou le service de cluster sont également arrêtés.</span><span class="sxs-lookup"><span data-stu-id="ba55d-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="ba55d-123">Les deux contrôleurs sont redémarrés lorsque vous entrez dans ce mode ou que vous le quittez.</span><span class="sxs-lookup"><span data-stu-id="ba55d-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="ba55d-124">Lorsque vous quittez le mode Maintenance, tous les services reprennent et doivent être sains.</span><span class="sxs-lookup"><span data-stu-id="ba55d-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="ba55d-125">Cela peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ba55d-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="ba55d-126">**Le mode Maintenance est uniquement pris en charge sur un appareil en état de fonctionnement. Il n’est pas pris en charge sur un appareil dont l’un ou les deux contrôleurs ne fonctionnent pas.**</span><span class="sxs-lookup"><span data-stu-id="ba55d-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="ba55d-127">Mode Récupération</span><span class="sxs-lookup"><span data-stu-id="ba55d-127">Recovery mode</span></span>

<span data-ttu-id="ba55d-128">Le mode Récupération peut être décrit comme un « mode sans échec avec prise en charge du réseau Windows ».</span><span class="sxs-lookup"><span data-stu-id="ba55d-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="ba55d-129">Le mode Récupération engage l’équipe de support technique Microsoft et leur permet d’effectuer des diagnostics sur le système.</span><span class="sxs-lookup"><span data-stu-id="ba55d-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="ba55d-130">L’objectif principal objectif du mode Récupération consiste à récupérer les journaux système.</span><span class="sxs-lookup"><span data-stu-id="ba55d-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="ba55d-131">Si votre système passe en mode Récupération, vous devez contacter le support technique Microsoft pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="ba55d-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="ba55d-132">Pour plus d’informations, accédez à [Contacter le support technique Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="ba55d-132">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ba55d-133">**Vous ne pouvez pas mettre l’appareil en mode Récupération. Si l’appareil est en mauvais état, ce mode tente de le rétablir dans un état permettant au support technique Microsoft de l’examiner.**</span><span class="sxs-lookup"><span data-stu-id="ba55d-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="ba55d-134">Détermination du mode de l’appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="ba55d-134">Determine StorSimple device mode</span></span>

#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="ba55d-135">Pour déterminer le mode actuel de l’appareil</span><span class="sxs-lookup"><span data-stu-id="ba55d-135">To determine the current device mode</span></span>

1. <span data-ttu-id="ba55d-136">Ouvrez une session sur la console série de l'appareil en suivant les étapes dans [Utilisation de PuTTY pour se connecter à la console série de l'appareil](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ba55d-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="ba55d-137">Examinez le message de bannière situé dans le menu de la console série de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ba55d-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="ba55d-138">Ce message indique explicitement si l’appareil est en mode Maintenance ou Récupération.</span><span class="sxs-lookup"><span data-stu-id="ba55d-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="ba55d-139">Si le message ne contient pas d’informations spécifiques sur le mode du système, l’appareil est en mode Normal.</span><span class="sxs-lookup"><span data-stu-id="ba55d-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="ba55d-140">Changer le mode de l'appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="ba55d-140">Change the StorSimple device mode</span></span>

<span data-ttu-id="ba55d-141">Vous pouvez mettre l’appareil StorSimple en mode Maintenance (à partir du mode Normal) pour effectuer une maintenance ou installer des mises à jour du mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ba55d-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="ba55d-142">Effectuez les procédures suivantes pour entrer dans le mode Maintenance ou le quitter.</span><span class="sxs-lookup"><span data-stu-id="ba55d-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba55d-143">Avant d’activer le mode Maintenance, vérifiez que les deux contrôleurs d’appareil fonctionnent correctement en accédant à **Paramètres > Hardware health** (Intégrité matérielle) pour votre appareil dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ba55d-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Device settings > Hardware health** for your device in the Azure portal.</span></span> <span data-ttu-id="ba55d-144">Si au moins l’un des deux contrôleurs n’est pas sain, contactez le Support Microsoft pour connaître les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="ba55d-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="ba55d-145">Pour plus d’informations, accédez à [Contacter le support technique Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="ba55d-145">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="ba55d-146">Pour passer en mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="ba55d-146">To enter maintenance mode</span></span>

1. <span data-ttu-id="ba55d-147">Ouvrez une session sur la console série de l'appareil en suivant les étapes dans [Utilisation de PuTTY pour se connecter à la console série de l'appareil](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ba55d-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="ba55d-148">Dans le menu de la console série, sélectionnez l’option 1, **Ouvrir une session avec un accès total**.</span><span class="sxs-lookup"><span data-stu-id="ba55d-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="ba55d-149">Lorsque vous y êtes invité, fournissez le **mot de passe administrateur de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="ba55d-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="ba55d-150">Le mot de passe par défaut est : `Password1`.</span><span class="sxs-lookup"><span data-stu-id="ba55d-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="ba55d-151">À l'invite de commandes, tapez</span><span class="sxs-lookup"><span data-stu-id="ba55d-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="ba55d-152">Un message d’avertissement s’affiche pour vous indiquer que le mode maintenance va perturber toutes les demandes d’E/S et annuler la connexion au portail Azure. Vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="ba55d-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="ba55d-153">Tapez **O** pour passer en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ba55d-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="ba55d-154">Les deux contrôleurs redémarrent.</span><span class="sxs-lookup"><span data-stu-id="ba55d-154">Both controllers will restart.</span></span> <span data-ttu-id="ba55d-155">Une fois le redémarrage terminé, la bannière de la console série indique que l’appareil est en mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="ba55d-155">When the restart is complete, the serial console banner will indicate that the device is in maintenance mode.</span></span> <span data-ttu-id="ba55d-156">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ba55d-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="ba55d-157">Pour quitter le mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="ba55d-157">To exit maintenance mode</span></span>

1. <span data-ttu-id="ba55d-158">Connectez-vous à la console série de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ba55d-158">Log on to the device serial console.</span></span> <span data-ttu-id="ba55d-159">Vérifiez dans le message de bannière, que votre appareil est en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ba55d-159">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="ba55d-160"> À l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="ba55d-160">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="ba55d-161">Un message d’avertissement et un message de confirmation s’affichent.</span><span class="sxs-lookup"><span data-stu-id="ba55d-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="ba55d-162">Tapez **O** pour quitter le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ba55d-162">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="ba55d-163">Les deux contrôleurs redémarrent.</span><span class="sxs-lookup"><span data-stu-id="ba55d-163">Both controllers will restart.</span></span> <span data-ttu-id="ba55d-164">Une fois le redémarrage terminé, la bannière de la console série indique que l’appareil est en mode normal.</span><span class="sxs-lookup"><span data-stu-id="ba55d-164">When the restart is complete, the serial console banner indicates that the device is in normal mode.</span></span> <span data-ttu-id="ba55d-165">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ba55d-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure to install on each controller could result in data corruption. Exiting maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to exit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="ba55d-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba55d-166">Next steps</span></span>

<span data-ttu-id="ba55d-167">Découvrez comment [appliquer les mises à jour des modes Normal et Maintenance](storsimple-update-device.md) sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ba55d-167">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

