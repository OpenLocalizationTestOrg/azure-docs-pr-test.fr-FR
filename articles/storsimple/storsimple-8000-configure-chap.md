---
title: "Configurer CHAP pour un appareil de la gamme StorSimple 8000 | Microsoft Docs"
description: "Décrit comment configurer le protocole Challenge Handshake Authentication Protocol (CHAP) sur un appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 61e0877187759d76b6f7efcef0a5ed8bec8500fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="7f73e-103">Configuration de CHAP pour votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="7f73e-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="7f73e-104">Ce didacticiel explique comment configurer CHAP pour votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f73e-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="7f73e-105">La procédure détaillée dans cet article s’applique aux appareils de la gamme StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="7f73e-105">The procedure detailed in this article applies to StorSimple 8000 series devices.</span></span>

<span data-ttu-id="7f73e-106">CHAP est l’abréviation de Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="7f73e-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="7f73e-107">Il s’agit d’un schéma d’authentification utilisé par les serveurs pour valider l’identité des clients distants.</span><span class="sxs-lookup"><span data-stu-id="7f73e-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="7f73e-108">La vérification repose sur un mot de passe partagé ou un secret.</span><span class="sxs-lookup"><span data-stu-id="7f73e-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="7f73e-109">Le protocole CHAP peut être à sens unique (unidirectionnel) ou mutuel (bidirectionnel).</span><span class="sxs-lookup"><span data-stu-id="7f73e-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="7f73e-110">Le protocole CHAP est unidirectionnel lorsque la cible authentifie un initiateur.</span><span class="sxs-lookup"><span data-stu-id="7f73e-110">One way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="7f73e-111">Dans l’authentification CHAP mutuelle ou inverse, la cible authentifie l’initiateur, puis l’initiateur authentifie la cible.</span><span class="sxs-lookup"><span data-stu-id="7f73e-111">In mutual or reverse CHAP, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="7f73e-112">L’authentification de l’initiateur peut être implémentée sans authentification cible.</span><span class="sxs-lookup"><span data-stu-id="7f73e-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="7f73e-113">Toutefois, l’authentification cible peut être implémentée uniquement si l’authentification de l’initiateur est également implémentée.</span><span class="sxs-lookup"><span data-stu-id="7f73e-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="7f73e-114">Nous vous recommandons d’utiliser CHAP pour améliorer la sécurité iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7f73e-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="7f73e-115">N’oubliez pas que IPSEC n’est pas actuellement pris en charge sur les appareils StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f73e-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="7f73e-116">Les paramètres CHAP sur l’appareil StorSimple peuvent être configurés comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f73e-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="7f73e-117">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="7f73e-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="7f73e-118">Authentification bidirectionnelle, mutuelle ou inverse</span><span class="sxs-lookup"><span data-stu-id="7f73e-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="7f73e-119">Dans chacun de ces cas, le portail pour l’appareil et le logiciel de l’initiateur iSCSI du serveur doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="7f73e-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="7f73e-120">Les étapes détaillées de cette configuration sont décrites dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7f73e-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="7f73e-121">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="7f73e-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="7f73e-122">Dans l’authentification unidirectionnelle, la cible authentifie l’initiateur.</span><span class="sxs-lookup"><span data-stu-id="7f73e-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="7f73e-123">Cette authentification nécessite de configurer les paramètres d’initiateur CHAP sur l’appareil StorSimple et le logiciel iSCSI Initiator sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="7f73e-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="7f73e-124">Les procédures détaillées pour votre appareil StorSimple et un hôte Windows sont décrites ci-après.</span><span class="sxs-lookup"><span data-stu-id="7f73e-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="7f73e-125">Configuration de votre appareil pour l’authentification unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="7f73e-125">To configure your device for one-way authentication</span></span>

1. <span data-ttu-id="7f73e-126">Dans le portail Azure, accédez à votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="7f73e-126">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="7f73e-127">Cliquez sur **Appareils**, puis sélectionnez et cliquez sur l’appareil pour lequel vous souhaitez configurer CHAP.</span><span class="sxs-lookup"><span data-stu-id="7f73e-127">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="7f73e-128">Accédez à **Paramètres de l’appareil > Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-128">Go to **Device settings > Security**.</span></span> <span data-ttu-id="7f73e-129">Dans le panneau **Paramètres de sécurité**, cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-129">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP Initiator](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="7f73e-131">Dans le panneau **CHAP**, puis dans la section **CHAP Initiator** :</span><span class="sxs-lookup"><span data-stu-id="7f73e-131">In the **CHAP** blade, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="7f73e-132">Indiquez un nom d’utilisateur pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="7f73e-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="7f73e-133">Spécifiez un mot de passe pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="7f73e-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="7f73e-134">Le nom d’utilisateur CHAP doit contenir moins de 233 caractères.</span><span class="sxs-lookup"><span data-stu-id="7f73e-134">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="7f73e-135">Le mot de passe CHAP doit comprendre entre 12 et 16 caractères.</span><span class="sxs-lookup"><span data-stu-id="7f73e-135">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="7f73e-136">L’utilisation d’un nom d’utilisateur ou d’un mot de passe plus long entraîne un échec d’authentification sur l’hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="7f73e-136">A longer user name or password results in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="7f73e-137">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7f73e-137">Confirm the password.</span></span>

       ![CHAP Initiator](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="7f73e-139">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-139">Click **Save**.</span></span> <span data-ttu-id="7f73e-140">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7f73e-140">A confirmation message is displayed.</span></span> <span data-ttu-id="7f73e-141">Cliquez sur **OK** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="7f73e-141">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="7f73e-142">Configuration de l’authentification unidirectionnelle sur le serveur hôte Windows</span><span class="sxs-lookup"><span data-stu-id="7f73e-142">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="7f73e-143">Sur le serveur hôte Windows, démarrez l’initiateur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7f73e-143">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="7f73e-144">Dans la fenêtre **iSCSI Initiator Properties** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f73e-144">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="7f73e-145">Cliquez sur l’onglet **Discovery** .</span><span class="sxs-lookup"><span data-stu-id="7f73e-145">Click the **Discovery** tab.</span></span>
      
       ![iSCSI Initiator Properties](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="7f73e-147">Cliquez sur **Discover Portal**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="7f73e-148">Dans la boîte de dialogue **Découvrir le portail cible** :</span><span class="sxs-lookup"><span data-stu-id="7f73e-148">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="7f73e-149">Spécifiez l’adresse IP de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f73e-149">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="7f73e-150">Cliquez sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-150">Click **Advanced**.</span></span>
      
       ![Découvrir le portail cible](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="7f73e-152">Dans la boîte de dialogue **Paramètres avancés** :</span><span class="sxs-lookup"><span data-stu-id="7f73e-152">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="7f73e-153">Cochez la case **Enable CHAP log on** .</span><span class="sxs-lookup"><span data-stu-id="7f73e-153">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="7f73e-154">Dans le champ **Nom** , tapez le nom d’utilisateur que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="7f73e-154">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="7f73e-155">Dans le champ **Secret de la cible** , fournissez le mot de passe que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="7f73e-155">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="7f73e-156">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-156">Click **OK**.</span></span>
      
       ![Paramètres avancés - Généraux](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="7f73e-158">Dans l’onglet **Targets** de la fenêtre **iSCSI Initiator Properties**, l’état de l’appareil devrait indiquer **Connected**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-158">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="7f73e-159">Si vous utilisez un appareil StorSimple 1200, chaque volume est monté en tant que cible iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7f73e-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="7f73e-160">Les étapes 3 et 4 doivent donc être répétées pour chaque volume.</span><span class="sxs-lookup"><span data-stu-id="7f73e-160">Hence, steps 3-4 will need to be repeated for each volume.</span></span>
   
    ![Volumes montés en tant que cibles distinctes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="7f73e-162">Si vous modifiez le nom iSCSI, le nouveau nom est utilisé pour les nouvelles sessions iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7f73e-162">If you change the iSCSI name, the new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="7f73e-163">Les nouveaux paramètres ne sont pas appliqués aux sessions existantes tant que vous n’avez pas quitté puis relancé la session.</span><span class="sxs-lookup"><span data-stu-id="7f73e-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="7f73e-164">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte Windows, voir la rubrique [Considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="7f73e-164">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="7f73e-165">Authentification bidirectionnelle ou mutuelle</span><span class="sxs-lookup"><span data-stu-id="7f73e-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="7f73e-166">Dans l’authentification bidirectionnelle, la cible authentifie l’initiateur, puis l’initiateur authentifie la cible.</span><span class="sxs-lookup"><span data-stu-id="7f73e-166">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="7f73e-167">Cette procédure oblige l’utilisateur à configurer les paramètres d’initiateur CHAP, les paramètres CHAP inverses sur l’appareil et le logiciel iSCSI Initiator sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="7f73e-167">This procedure requires the user to configure the CHAP initiator settings, reverse CHAP settings on the device, and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="7f73e-168">Les procédures suivantes décrivent les étapes pour configurer l’authentification mutuelle sur l’appareil et sur l’hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="7f73e-168">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="7f73e-169">Configuration de votre appareil pour l’authentification mutuelle</span><span class="sxs-lookup"><span data-stu-id="7f73e-169">To configure your device for mutual authentication</span></span>

1. <span data-ttu-id="7f73e-170">Dans le portail Azure, accédez à votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="7f73e-170">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="7f73e-171">Cliquez sur **Appareils**, puis sélectionnez et cliquez sur l’appareil pour lequel vous souhaitez configurer CHAP.</span><span class="sxs-lookup"><span data-stu-id="7f73e-171">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="7f73e-172">Accédez à **Paramètres de l’appareil > Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-172">Go to **Device settings > Security**.</span></span> <span data-ttu-id="7f73e-173">Dans le panneau **Paramètres de sécurité**, cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-173">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP Target](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="7f73e-175">Faites défiler cette page vers le bas, puis dans la section **CHAP Target** :</span><span class="sxs-lookup"><span data-stu-id="7f73e-175">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="7f73e-176">Indiquez le **nom d’utilisateur CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f73e-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="7f73e-177">Indiquez le **mot de passe CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f73e-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="7f73e-178">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7f73e-178">Confirm the password.</span></span>
3. <span data-ttu-id="7f73e-179">Dans la section **CHAP Initiator** :</span><span class="sxs-lookup"><span data-stu-id="7f73e-179">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="7f73e-180">Indiquez un **nom d’utilisateur** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f73e-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="7f73e-181">Indiquez un **mot de passe** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f73e-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="7f73e-182">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7f73e-182">Confirm the password.</span></span>

       ![CHAP Initiator](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="7f73e-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-184">Click **Save**.</span></span> <span data-ttu-id="7f73e-185">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7f73e-185">A confirmation message is displayed.</span></span> <span data-ttu-id="7f73e-186">Cliquez sur **OK** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="7f73e-186">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="7f73e-187">Configuration de l’authentification bidirectionnelle sur le serveur hôte Windows</span><span class="sxs-lookup"><span data-stu-id="7f73e-187">To configure bidirectional authentication on the Windows host server</span></span>

1. <span data-ttu-id="7f73e-188">Sur le serveur hôte Windows, démarrez l’initiateur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7f73e-188">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="7f73e-189">Dans la fenêtre **iSCSI Initiator Properties**, cliquez sur l’onglet **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-189">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="7f73e-190">Cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="7f73e-191">Dans la boîte de dialogue **Secret CHAP mutuel de l’initiateur iSCSI** :</span><span class="sxs-lookup"><span data-stu-id="7f73e-191">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="7f73e-192">Entrez le **mot de passe CHAP inverse** que vous avez configuré dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f73e-192">Type the **Reverse CHAP Password** that you configured in the Azure portal.</span></span>
   2. <span data-ttu-id="7f73e-193">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-193">Click **OK**.</span></span>
      
       ![Secret CHAP mutuel de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="7f73e-195">Cliquez sur l’onglet **Targets** .</span><span class="sxs-lookup"><span data-stu-id="7f73e-195">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="7f73e-196">Cliquez sur le bouton **Connect** .</span><span class="sxs-lookup"><span data-stu-id="7f73e-196">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="7f73e-197">Dans la boîte de dialogue **Se connecter à la cible**, cliquez sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-197">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="7f73e-198">Dans la boîte de dialogue **Advanced Properties** :</span><span class="sxs-lookup"><span data-stu-id="7f73e-198">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="7f73e-199">Cochez la case **Enable CHAP log on** .</span><span class="sxs-lookup"><span data-stu-id="7f73e-199">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="7f73e-200">Dans le champ **Nom** , tapez le nom d’utilisateur que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="7f73e-200">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="7f73e-201">Dans le champ **Secret de la cible** , fournissez le mot de passe que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="7f73e-201">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="7f73e-202">Cochez la case **Perform mutual authentication** .</span><span class="sxs-lookup"><span data-stu-id="7f73e-202">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Paramètres avancés - Authentification mutuelle](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="7f73e-204">Cliquez sur **OK** pour terminer la configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="7f73e-204">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="7f73e-205">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte Windows, voir la rubrique [Considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="7f73e-205">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="7f73e-206">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7f73e-206">Additional considerations</span></span>

<span data-ttu-id="7f73e-207">La fonctionnalité **Quick Connect** ne prend pas en charge les connexions pour lesquelles le protocole CHAP est activé.</span><span class="sxs-lookup"><span data-stu-id="7f73e-207">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="7f73e-208">Lorsque le protocole CHAP est activé, assurez-vous d’utiliser le bouton **Connect** disponible dans l’onglet **Targets** pour vous connecter à une cible.</span><span class="sxs-lookup"><span data-stu-id="7f73e-208">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Se connecter à la cible](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="7f73e-210">Dans la boîte de dialogue **Se connecter à la cible** qui s’affiche, cochez la case **Add this connection to the list of Favorite Targets**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-210">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="7f73e-211">Cette sélection garantit que chaque fois que l’ordinateur redémarre, une tentative est effectuée pour rétablir la connexion aux cibles iSCSI favorites.</span><span class="sxs-lookup"><span data-stu-id="7f73e-211">This selection ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="7f73e-212">Erreurs lors de la configuration</span><span class="sxs-lookup"><span data-stu-id="7f73e-212">Errors during configuration</span></span>

<span data-ttu-id="7f73e-213">Si votre configuration CHAP est incorrecte, un message d’erreur d’ **échec de l’authentification** risque d’apparaître.</span><span class="sxs-lookup"><span data-stu-id="7f73e-213">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="7f73e-214">Vérification de la configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="7f73e-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="7f73e-215">Vous pouvez vérifier que le protocole CHAP est utilisé en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="7f73e-215">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="7f73e-216">Vérification de votre configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="7f73e-216">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="7f73e-217">Cliquez sur **Favorite Targets**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="7f73e-218">Sélectionnez la cible pour laquelle vous avez activé l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7f73e-218">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="7f73e-219">Cliquez sur **Details**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-219">Click **Details**.</span></span>
   
    ![Cibles favorites des propriétés de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="7f73e-221">Dans la boîte de dialogue **Favorite Target Details**, notez l’entrée figurant dans le champ **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-221">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="7f73e-222">Si la configuration a réussi, le champ devrait afficher **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7f73e-222">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Détails sur les cibles favorites](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="7f73e-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f73e-224">Next steps</span></span>

* <span data-ttu-id="7f73e-225">En savoir plus sur la [sécurité StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="7f73e-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="7f73e-226">En savoir plus sur l’[utilisation du service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7f73e-226">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

