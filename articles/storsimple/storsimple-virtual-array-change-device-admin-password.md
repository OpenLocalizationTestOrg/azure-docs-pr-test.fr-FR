---
title: "mot de passe de l’administrateur d’appareil aaaChange StorSimple Virtual Array | Documents Microsoft"
description: "Décrit comment toouse hello soit portail Azure ou StorSimple Virtual Array web UI toochange hello appareil mot de passe administrateur."
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
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="bbb9d-103">Modifier le mot de passe hello StorSimple Virtual Array appareil administrateur via le Gestionnaire de périphériques StorSimple</span><span class="sxs-lookup"><span data-stu-id="bbb9d-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="bbb9d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bbb9d-104">Overview</span></span>

<span data-ttu-id="bbb9d-105">Lorsque vous utilisez hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, vous êtes tooenter requis un mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="bbb9d-106">Lorsque l’appareil StorSimple hello est tout d’abord configuré et démarré, le mot de passe par défaut hello est *Password1*.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="bbb9d-107">Pour une sécurité hello de vos données, un mot de passe par défaut hello expire hello première fois que vous vous connectez et vous est requis toochange ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="bbb9d-108">Vous pouvez également utiliser soit hello web local UI ou hello toochange portail Azure hello appareil administrateur mot de passe à tout moment une fois l’appareil de hello est déployé dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="bbb9d-109">Chacune de ces procédures est décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-109">Each of these procedures is described in this article.</span></span>

 ![Panneau Appareils](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="bbb9d-111">Mot de passe hello hello toochange portail Azure</span><span class="sxs-lookup"><span data-stu-id="bbb9d-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="bbb9d-112">Effectuer hello suivant les étapes toochange hello appareil mot de passe administrateur via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="bbb9d-113">mot de passe administrateur toochange pour hello appareil via hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bbb9d-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="bbb9d-114">Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **gestion** , cliquez sur **périphériques**.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="bbb9d-115">Cette opération ouvre hello **périphériques** panneau qui répertorie tous vos appareils StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="bbb9d-116">Bonjour **périphériques** panneau, double-cliquez sur le périphérique hello qui nécessite un changement de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="bbb9d-117">Bonjour **paramètres** panneau pour votre appareil, cliquez sur **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="bbb9d-118">Bonjour **paramètres de sécurité** panneau, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="bbb9d-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="bbb9d-119">Faites défiler vers le bas toohello **mot de passe administrateur de l’appareil** section.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="bbb9d-120">Fournir un mot de passe administrateur contenant entre 8 caractères too15.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="bbb9d-121">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="bbb9d-122">Cliquez sur **enregistrer** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="bbb9d-123">mise à jour de mot de passe administrateur de périphérique Hello.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="bbb9d-124">Vous pouvez utiliser ce périphérique de hello tooaccess mot de passe modifié localement.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-124">You can use this modified password tooaccess hello device locally.</span></span>

![Panneau Paramètres de sécurité](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="bbb9d-126">Utilisez hello web local UI toochange hello mot de passe</span><span class="sxs-lookup"><span data-stu-id="bbb9d-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="bbb9d-127">Effectuer hello suivant les étapes toochange hello appareil mot de passe administrateur via l’interface utilisateur de web locale hello.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="bbb9d-128">mot de passe administrateur toochange pour hello appareil via l’interface utilisateur de web locale hello</span><span class="sxs-lookup"><span data-stu-id="bbb9d-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="bbb9d-129">Dans l’interface utilisateur de web locale hello, cliquez sur **Maintenance** > **modification de mot de passe** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![change password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="bbb9d-131">Entrez hello **mot de passe actuel**.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="bbb9d-132">Fournissez un **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-132">Provide a **New Password**.</span></span> <span data-ttu-id="bbb9d-133">mot de passe Hello doit être au moins 8 caractères.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="bbb9d-134">Il doit contenir 3 des 4 suivants de hello : caractères majuscules, minuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="bbb9d-135">Notez que votre mot de passe ne peut pas être hello identique hello derniers 24 mots de passe.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="bbb9d-136">Entrez à nouveau tooconfirm de mot de passe hello il.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-136">Reenter hello password tooconfirm it.</span></span>
   
    ![change password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="bbb9d-138">Au bas de hello de page de hello, cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="bbb9d-139">nouveau mot de passe Hello est maintenant appliquée.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-139">hello new password is now applied.</span></span> <span data-ttu-id="bbb9d-140">Si la modification de mot de passe hello ne réussit pas, vous consultez hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="bbb9d-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![password error](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="bbb9d-142">Une fois le mot de passe hello est correctement mise à jour, vous êtes averti.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="bbb9d-143">Vous pouvez ensuite utiliser ce périphérique de hello tooaccess mot de passe modifié localement.</span><span class="sxs-lookup"><span data-stu-id="bbb9d-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bbb9d-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bbb9d-144">Next steps</span></span>
<span data-ttu-id="bbb9d-145">Découvrez comment trop[administrer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="bbb9d-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

