---
title: aaaChange vos mots de passe StorSimple | Documents Microsoft
description: "Décrit comment toouse hello toochange du service Gestionnaire de périphériques StorSimple vos mots de passe d’administrateur de gestionnaire d’instantanés StorSimple et de périphérique."
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
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="bca38-103">Utilisez hello le Gestionnaire de périphériques StorSimple service toochange vos mots de passe StorSimple</span><span class="sxs-lookup"><span data-stu-id="bca38-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="bca38-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bca38-104">Overview</span></span>
<span data-ttu-id="bca38-105">Bonjour Azure portal **paramètres de périphérique** option contienne tous les paramètres de périphérique hello que vous pouvez reconfigurer sur un appareil StorSimple qui est géré par un service Gestionnaire de périphériques StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bca38-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="bca38-106">Ce didacticiel explique comment vous pouvez utiliser hello **sécurité** sous **paramètres de périphérique** toochange votre administrateur de l’appareil ou le mot de passe de gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bca38-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="bca38-107">Mot de passe de l’administrateur d’appareil modification hello</span><span class="sxs-lookup"><span data-stu-id="bca38-107">Change hello device administrator password</span></span>
<span data-ttu-id="bca38-108">Lorsque vous utilisez Windows PowerShell interface tooaccess hello StorSimple, vous êtes tooenter requis un mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="bca38-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="bca38-109">Lorsque l’appareil StorSimple première hello est inscrit auprès d’un service, un mot de passe par défaut hello pour cette interface est *Password1*.</span><span class="sxs-lookup"><span data-stu-id="bca38-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="bca38-110">Sécurité hello de vos données, vous êtes toochange requis ce mot de passe à fin hello du processus d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="bca38-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="bca38-111">Vous ne pouvez pas quitter processus d’inscription de hello sans modifier ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="bca38-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="bca38-112">Pour plus d’informations, consultez [étape 3 : configurer et inscrire l’appareil hello via Windows PowerShell pour StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="bca38-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="bca38-113">mot de passe Hello tout d’abord défini via l’interface Windows PowerShell de hello lors de l’inscription peut être modifié ultérieurement via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bca38-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="bca38-114">Effectuer hello suivant les étapes toochange hello administrateur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="bca38-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="bca38-115">mot de passe de l’administrateur d’appareil toochange hello</span><span class="sxs-lookup"><span data-stu-id="bca38-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="bca38-116">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**.</span><span class="sxs-lookup"><span data-stu-id="bca38-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="bca38-117">À partir de hello tabulaire la liste des périphériques, sélectionnez et cliquez sur périphérique de hello dont un mot de passe vous avez l’intention de toochange.</span><span class="sxs-lookup"><span data-stu-id="bca38-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="bca38-118">Bonjour **paramètres** panneau, accédez trop**paramètres du périphérique > sécurité**.</span><span class="sxs-lookup"><span data-stu-id="bca38-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="bca38-119">Bonjour **paramètres de sécurité** panneau, cliquez sur **mot de passe** mot de passe de l’administrateur d’appareil toochange hello.</span><span class="sxs-lookup"><span data-stu-id="bca38-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="bca38-120">Bonjour **mot de passe** panneau, fournir un mot de passe administrateur contenant entre 8 caractères too15.</span><span class="sxs-lookup"><span data-stu-id="bca38-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="bca38-121">mot de passe Hello doit être une combinaison d’au moins 3 caractères majuscules, minuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="bca38-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="bca38-122">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="bca38-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="bca38-123">Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="bca38-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="bca38-124">mot de passe administrateur Hello périphérique doit maintenant être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="bca38-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="bca38-125">Vous pouvez utiliser cette interface Windows PowerShell de mot de passe modifié tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="bca38-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="bca38-126">Mot de passe de gestionnaire d’instantanés StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="bca38-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="bca38-127">Gestionnaire d’instantanés StorSimple logiciel réside sur l’hôte Windows et permet aux administrateurs toomanage les sauvegardes de votre appareil StorSimple dans l’écran hello locaux et les instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="bca38-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="bca38-128">Lorsque vous configurez un appareil de gestionnaire d’instantanés StorSimple, vous serez invité tooprovide hello IP adresse et le mot de passe tooauthenticate d’appareil de votre périphérique de stockage.</span><span class="sxs-lookup"><span data-stu-id="bca38-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="bca38-129">Vous pouvez définir ou modifier un mot de passe hello Gestionnaire d’instantanés StorSimple via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bca38-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="bca38-130">Effectuer hello suivant les étapes tooset ou modifier le mot de passe de gestionnaire d’instantanés StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="bca38-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="bca38-131">mot de passe tooset hello Gestionnaire d’instantanés StorSimple</span><span class="sxs-lookup"><span data-stu-id="bca38-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="bca38-132">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**.</span><span class="sxs-lookup"><span data-stu-id="bca38-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="bca38-133">À partir de hello tabulaire la liste des périphériques, sélectionnez et cliquez sur le périphérique de hello dont mot de passe de gestionnaire d’instantanés StorSimple vous avez l’intention tooset ou modifiez.</span><span class="sxs-lookup"><span data-stu-id="bca38-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="bca38-134">Bonjour **paramètres** panneau, accédez trop**paramètres du périphérique > sécurité**.</span><span class="sxs-lookup"><span data-stu-id="bca38-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="bca38-135">Bonjour **paramètres de sécurité** panneau, cliquez sur **mot de passe** tooset ou modification de mot de passe de gestionnaire d’instantanés StorSimple de hello.</span><span class="sxs-lookup"><span data-stu-id="bca38-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="bca38-136">Bonjour **mot de passe** panneau, entrez un mot de passe de 14 ou 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="bca38-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="bca38-137">Assurez-vous que ce mot de passe hello contienne une combinaison d’au moins 3 caractères majuscules, minuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="bca38-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="bca38-138">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="bca38-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="bca38-139">Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="bca38-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="bca38-140">mot de passe de gestionnaire d’instantanés StorSimple Hello doit maintenant être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="bca38-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bca38-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bca38-141">Next steps</span></span>
* <span data-ttu-id="bca38-142">En savoir plus sur la [sécurité StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="bca38-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="bca38-143">En savoir plus sur la [modification de la configuration de votre appareil](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="bca38-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="bca38-144">En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bca38-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

