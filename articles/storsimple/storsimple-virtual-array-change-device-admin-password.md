---
title: "Modifier le mot de passe administrateur de l’appareil StorSimple Virtual Array | Microsoft Docs"
description: "Explique comment utiliser le portail Azure ou l’interface utilisateur web de StorSimple Virtual Array pour modifier le mot de passe administrateur de l’appareil."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="6876e-103">Modifier le mot de passe administrateur de l’appareil StorSimple Virtual Array via StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="6876e-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="6876e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6876e-104">Overview</span></span>

<span data-ttu-id="6876e-105">Quand vous utilisez l’interface Windows PowerShell pour accéder au StorSimple Virtual Array, vous devez entrer un mot de passe administrateur pour l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6876e-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="6876e-106">Lorsque l'appareil StorSimple est d'abord configuré puis démarré, le mot de passe par défaut est *Password1*.</span><span class="sxs-lookup"><span data-stu-id="6876e-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="6876e-107">Pour garantir la sécurité de vos données, le mot de passe par défaut expire dès votre première connexion et vous devez donc le modifier.</span><span class="sxs-lookup"><span data-stu-id="6876e-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="6876e-108">Vous pouvez également utiliser l’interface utilisateur web locale ou le portail Azure pour modifier à tout moment le mot de passe administrateur une fois l’appareil déployé dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6876e-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="6876e-109">Chacune de ces procédures est décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6876e-109">Each of these procedures is described in this article.</span></span>

 ![Panneau Appareils](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="6876e-111">Utiliser le portail Azure pour modifier le mot de passe</span><span class="sxs-lookup"><span data-stu-id="6876e-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="6876e-112">Procédez comme suit pour modifier le mot de passe administrateur de l’appareil via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6876e-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="6876e-113">Pour modifier le mot de passe administrateur de l’appareil via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6876e-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="6876e-114">Dans la page d’accueil du service, sélectionnez votre service, double-cliquez sur le nom du service, puis dans la section **Gestion**, cliquez sur **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="6876e-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="6876e-115">Le panneau **Appareils**, qui répertorie tous vos appareils StorSimple Virtual Array, s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="6876e-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="6876e-116">Dans le panneau **Appareils**, double-cliquez sur l’appareil dont le mot de passe doit être modifié.</span><span class="sxs-lookup"><span data-stu-id="6876e-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="6876e-117">Dans le panneau **Paramètres** de votre appareil, cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="6876e-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="6876e-118">Dans le panneau **Paramètres de sécurité**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6876e-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="6876e-119">Faites défiler l’écran vers le bas jusqu’à la section **Mot de passe de l’administrateur de l’appareil** .</span><span class="sxs-lookup"><span data-stu-id="6876e-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="6876e-120">Indiquez un mot de passe Administrateur contenant entre 8 et 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="6876e-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="6876e-121">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6876e-121">Confirm the password.</span></span>
   3. <span data-ttu-id="6876e-122">Cliquez sur **Enregistrer** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="6876e-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="6876e-123">Le mot de passe administrateur de l’appareil est maintenant à jour.</span><span class="sxs-lookup"><span data-stu-id="6876e-123">The device administrator password is now updated.</span></span> <span data-ttu-id="6876e-124">Vous pouvez utiliser ce mot de passe modifié pour accéder à l’appareil localement.</span><span class="sxs-lookup"><span data-stu-id="6876e-124">You can use this modified password to access the device locally.</span></span>

![Panneau Paramètres de sécurité](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="6876e-126">Utiliser l’interface utilisateur web locale pour modifier le mot de passe</span><span class="sxs-lookup"><span data-stu-id="6876e-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="6876e-127">Procédez comme suit pour modifier le mot de passe d’administrateur de l’appareil via l’interface utilisateur web locale.</span><span class="sxs-lookup"><span data-stu-id="6876e-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="6876e-128">Pour modifier le mot de passe administrateur de l’appareil via l’interface utilisateur web locale</span><span class="sxs-lookup"><span data-stu-id="6876e-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="6876e-129">Dans l’interface utilisateur web locale, cliquez sur **Maintenance** > **Modifier le mot de passe** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="6876e-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![change password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="6876e-131">Entrez le **mot de passe actuel**.</span><span class="sxs-lookup"><span data-stu-id="6876e-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="6876e-132">Fournissez un **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6876e-132">Provide a **New Password**.</span></span> <span data-ttu-id="6876e-133">Le mot de passe doit comporter au moins 8 caractères.</span><span class="sxs-lookup"><span data-stu-id="6876e-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="6876e-134">Il doit contenir 3 caractères sur 4 en majuscules, minuscules, chiffres et caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="6876e-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="6876e-135">Notez que votre mot de passe ne peut pas être identique aux 24 derniers mots de passe.</span><span class="sxs-lookup"><span data-stu-id="6876e-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="6876e-136">Entrez de nouveau le mot de passe pour le confirmer.</span><span class="sxs-lookup"><span data-stu-id="6876e-136">Reenter the password to confirm it.</span></span>
   
    ![change password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="6876e-138">En bas de cette page, cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="6876e-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="6876e-139">Le nouveau mot de passe est maintenant appliqué.</span><span class="sxs-lookup"><span data-stu-id="6876e-139">The new password is now applied.</span></span> <span data-ttu-id="6876e-140">Si la modification du mot de passe échoue, l’erreur suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="6876e-140">If the password change is not successful, you see the following error:</span></span>
   
    ![password error](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="6876e-142">Vous êtes averti une fois le mot de passe correctement mis à jour.</span><span class="sxs-lookup"><span data-stu-id="6876e-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="6876e-143">Vous pouvez ensuite utiliser ce mot de passe modifié pour accéder à l’appareil localement.</span><span class="sxs-lookup"><span data-stu-id="6876e-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6876e-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6876e-144">Next steps</span></span>
<span data-ttu-id="6876e-145">Découvrez comment [gérer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="6876e-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

