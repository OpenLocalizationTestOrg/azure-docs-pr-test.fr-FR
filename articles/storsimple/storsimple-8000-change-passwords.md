---
title: Modification de vos mots de passe StorSimple | Microsoft Docs
description: "Explique comment utiliser le service StorSimple Device Manager pour modifier vos mots de passe du Gestionnaire d’instantanés StorSimple et d’administrateur de l’appareil."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 7762f8499c67672f0a2ffed99e98baea4c940fa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="5e374-103">Utilisation du service StorSimple Device Manager pour modifier vos mots de passe StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e374-103">Use the StorSimple Device Manager service to change your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="5e374-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5e374-104">Overview</span></span>
<span data-ttu-id="5e374-105">L’option **Configurer** du portail Azure contient tous les paramètres d’appareil que vous pouvez reconfigurer sur un appareil StorSimple géré par un service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="5e374-105">The Azure portal **Device settings** option contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="5e374-106">Ce didacticiel explique comment utiliser l’option **Sécurité** sous **Paramètres de l’appareil** pour modifier le mot de passe d’administrateur de l’appareil ou le mot de passe du Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5e374-106">This tutorial explains how you can use the **Security** option under **Device settings** to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="5e374-107">Modification du mot de passe d’administrateur de l’appareil</span><span class="sxs-lookup"><span data-stu-id="5e374-107">Change the device administrator password</span></span>
<span data-ttu-id="5e374-108">Quand vous utilisez l’interface Windows PowerShell pour accéder à l’appareil StorSimple, vous devez entrer un mot de passe d’administrateur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="5e374-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="5e374-109">À l’inscription du premier appareil StorSimple auprès d’un service, le mot de passe par défaut de cette interface est *Password1*.</span><span class="sxs-lookup"><span data-stu-id="5e374-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="5e374-110">Pour assurer la sécurité de vos données, il vous est demandé de modifier ce mot de passe à la fin de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="5e374-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="5e374-111">Vous ne pouvez pas quitter le processus d'inscription sans modifier ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e374-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="5e374-112">Pour plus d’informations, voir [Étape 3 : Configuration et inscription de l’appareil via Windows PowerShell pour StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="5e374-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="5e374-113">Le mot de passe qui a été défini initialement dans l’interface Windows PowerShell au moment de l’inscription peut être modifié ultérieurement via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5e374-113">The password that was first set through the Windows PowerShell interface during registration can be changed later via the Azure portal.</span></span> <span data-ttu-id="5e374-114">Pour modifier le mot de passe d’administrateur de l’appareil, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="5e374-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="5e374-115">Pour modifier le mot de passe d’administrateur de l’appareil</span><span class="sxs-lookup"><span data-stu-id="5e374-115">To change the device administrator password</span></span>
1. <span data-ttu-id="5e374-116">Accédez à votre service StorSimple Device Manager et cliquez sur **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="5e374-116">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="5e374-117">Dans la liste tabulaire d’appareils, sélectionnez et cliquez sur l’appareil dont vous souhaitez modifier le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e374-117">From the tabular listing of devices, select and click the device whose password you intend to change.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="5e374-118">Dans le panneau **Paramètres**, accédez à **Paramètres de l’appareil > Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="5e374-118">In the **Settings** blade, go to **Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="5e374-119">Dans le panneau **Paramètres de sécurité**, cliquez sur **Mot de passe** pour modifier le mot de passe d’administrateur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="5e374-119">In the **Security settings** blade, click **Password** to change the device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="5e374-120">Dans le panneau **Mot de passe**, indiquez un mot de passe d’administrateur contenant entre 8 et 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="5e374-120">In the **Password** blade, provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="5e374-121">Le mot de passe doit contenir une combinaison d’au moins 3 caractères en majuscules, en minuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="5e374-121">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="5e374-122">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e374-122">Confirm the password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="5e374-123">Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="5e374-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="5e374-124">Le mot de passe Administrateur d’appareil doit maintenant être à jour.</span><span class="sxs-lookup"><span data-stu-id="5e374-124">The device administrator password should now be updated.</span></span> <span data-ttu-id="5e374-125">Vous pouvez utiliser ce mot de passe modifié pour accéder à l’interface Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e374-125">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="5e374-126">Définition du mot de passe du Gestionnaire d’instantanés StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e374-126">Set the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="5e374-127">Le Gestionnaire d’instantanés StorSimple réside sur l’ordinateur hôte Windows et permet aux administrateurs de gérer les sauvegardes de votre appareil StorSimple sous la forme d’instantanés cloud ou locaux.</span><span class="sxs-lookup"><span data-stu-id="5e374-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="5e374-128">Au moment de configurer un appareil dans le Gestionnaire d’instantanés StorSimple, vous êtes invité à fournir l’adresse IP et le mot de passe de votre appareil de stockage afin de l’authentifier.</span><span class="sxs-lookup"><span data-stu-id="5e374-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span>

<span data-ttu-id="5e374-129">Vous pouvez définir ou modifier le mot de passe du Gestionnaire d’instantanés StorSimple via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5e374-129">You can set or change the password for StorSimple Snapshot Manager via the Azure portal.</span></span> <span data-ttu-id="5e374-130">Procédez comme suit pour définir ou modifier le mot de passe du Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5e374-130">Perform the following steps to set or change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="5e374-131">Pour définir le mot de passe du Gestionnaire d’instantanés StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e374-131">To set the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="5e374-132">Accédez à votre service StorSimple Device Manager et cliquez sur **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="5e374-132">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="5e374-133">Dans la liste tabulaire d’appareils, sélectionnez et cliquez sur l’appareil dont vous souhaitez définir ou modifier le mot de passe du Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5e374-133">From the tabular listing of devices, select and click the device whose StorSimple Snapshot Manager password you intend to set or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="5e374-134">Dans le panneau **Paramètres**, accédez à **Paramètres de l’appareil > Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="5e374-134">In the **Settings** blade, go to **Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="5e374-135">Dans le panneau **Paramètres de sécurité**, cliquez sur **Mot de passe** pour définir ou modifier le mot de passe du Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5e374-135">In the **Security settings** blade, click **Password** to set or change the StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="5e374-136">Dans le panneau **Mot de passe**, entrez un mot de passe de 14 ou 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="5e374-136">In the **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="5e374-137">Assurez-vous que le mot de passe contient une combinaison d’au moins 3 caractères en majuscules, en minuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="5e374-137">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="5e374-138">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e374-138">Confirm the password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="5e374-139">Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="5e374-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="5e374-140">Le mot de passe du Gestionnaire d’instantanés StorSimple doit maintenant être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5e374-140">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e374-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e374-141">Next steps</span></span>
* <span data-ttu-id="5e374-142">En savoir plus sur la [sécurité StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="5e374-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="5e374-143">En savoir plus sur la [modification de la configuration de votre appareil](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="5e374-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="5e374-144">En savoir plus sur [l’utilisation du service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5e374-144">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

