---
title: "Configurer CHAP pour un appareil de la gamme StorSimple 8000 | Microsoft Docs"
description: "Décrit comment configurer le protocole Challenge Handshake Authentication Protocol (CHAP) sur un appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 36b4e73d0336deb9560d44163fc5330d1c9d775c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="81650-103">Configuration de CHAP pour votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="81650-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="81650-104">Ce didacticiel explique comment configurer CHAP pour votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="81650-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="81650-105">La procédure détaillée dans cet article s’applique aux appareils StorSimple série 8000, ainsi qu’aux appareils StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="81650-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="81650-106">CHAP est l’abréviation de Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="81650-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="81650-107">Il s’agit d’un schéma d’authentification utilisé par les serveurs pour valider l’identité des clients distants.</span><span class="sxs-lookup"><span data-stu-id="81650-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="81650-108">La vérification repose sur un mot de passe partagé ou un secret.</span><span class="sxs-lookup"><span data-stu-id="81650-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="81650-109">Le protocole CHAP peut être à sens unique (unidirectionnel) ou mutuel (bidirectionnel).</span><span class="sxs-lookup"><span data-stu-id="81650-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="81650-110">Le protocole CHAP est unidirectionnel lorsque la cible authentifie un initiateur.</span><span class="sxs-lookup"><span data-stu-id="81650-110">One-way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="81650-111">Par opposition, l’authentification CHAP mutuelle ou inverse nécessite que la cible authentifie l’initiateur, puis que l’initiateur authentifie la cible.</span><span class="sxs-lookup"><span data-stu-id="81650-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span></span> <span data-ttu-id="81650-112">L’authentification de l’initiateur peut être implémentée sans authentification cible.</span><span class="sxs-lookup"><span data-stu-id="81650-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="81650-113">Toutefois, l’authentification cible peut être implémentée uniquement si l’authentification de l’initiateur est également implémentée.</span><span class="sxs-lookup"><span data-stu-id="81650-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="81650-114">Nous vous recommandons d’utiliser CHAP pour améliorer la sécurité iSCSI.</span><span class="sxs-lookup"><span data-stu-id="81650-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="81650-115">N’oubliez pas que IPSEC n’est pas actuellement pris en charge sur les appareils StorSimple.</span><span class="sxs-lookup"><span data-stu-id="81650-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="81650-116">Les paramètres CHAP sur l’appareil StorSimple peuvent être configurés comme suit :</span><span class="sxs-lookup"><span data-stu-id="81650-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="81650-117">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="81650-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="81650-118">Authentification bidirectionnelle, mutuelle ou inverse</span><span class="sxs-lookup"><span data-stu-id="81650-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="81650-119">Dans chacun de ces cas, le portail pour l’appareil et le logiciel de l’initiateur iSCSI du serveur doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="81650-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="81650-120">Les étapes détaillées de cette configuration sont décrites dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="81650-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="81650-121">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="81650-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="81650-122">Dans l’authentification unidirectionnelle, la cible authentifie l’initiateur.</span><span class="sxs-lookup"><span data-stu-id="81650-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="81650-123">Cette authentification nécessite de configurer les paramètres d’initiateur CHAP sur l’appareil StorSimple et le logiciel iSCSI Initiator sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="81650-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="81650-124">Les procédures détaillées pour votre appareil StorSimple et un hôte Windows sont décrites ci-après.</span><span class="sxs-lookup"><span data-stu-id="81650-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="81650-125">Configuration de votre appareil pour l’authentification unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="81650-125">To configure your device for one-way authentication</span></span>
1. <span data-ttu-id="81650-126">Dans le portail Azure Classic, sur la page **Appareils**, cliquez sur l’onglet **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="81650-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP Initiator](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="81650-128">Faites défiler cette page vers le bas, puis dans la section **CHAP Initiator** :</span><span class="sxs-lookup"><span data-stu-id="81650-128">Scroll down on this page, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="81650-129">Indiquez un nom d’utilisateur pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="81650-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="81650-130">Spécifiez un mot de passe pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="81650-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="81650-131">Le nom d’utilisateur CHAP doit contenir moins de 233 caractères.</span><span class="sxs-lookup"><span data-stu-id="81650-131">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="81650-132">Le mot de passe CHAP doit comprendre entre 12 et 16 caractères.</span><span class="sxs-lookup"><span data-stu-id="81650-132">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="81650-133">L’utilisation d’un nom d’utilisateur ou d’un mot de passe plus long entraîne un échec d’authentification sur l’hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="81650-133">A longer user name or password will result in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="81650-134">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="81650-134">Confirm the password.</span></span>
3. <span data-ttu-id="81650-135">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="81650-135">Click **Save**.</span></span> <span data-ttu-id="81650-136">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="81650-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="81650-137">Cliquez sur **OK** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="81650-137">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="81650-138">Configuration de l’authentification unidirectionnelle sur le serveur hôte Windows</span><span class="sxs-lookup"><span data-stu-id="81650-138">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="81650-139">Sur le serveur hôte Windows, démarrez l’initiateur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="81650-139">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="81650-140">Dans la fenêtre **iSCSI Initiator Properties** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="81650-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="81650-141">Cliquez sur l’onglet **Discovery** .</span><span class="sxs-lookup"><span data-stu-id="81650-141">Click the **Discovery** tab.</span></span>
      
       ![iSCSI Initiator Properties](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="81650-143">Cliquez sur **Discover Portal**.</span><span class="sxs-lookup"><span data-stu-id="81650-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="81650-144">Dans la boîte de dialogue **Découvrir le portail cible** :</span><span class="sxs-lookup"><span data-stu-id="81650-144">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="81650-145">Spécifiez l’adresse IP de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81650-145">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="81650-146">Cliquez sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="81650-146">Click **Advanced**.</span></span>
      
       ![Découvrir le portail cible](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="81650-148">Dans la boîte de dialogue **Paramètres avancés** :</span><span class="sxs-lookup"><span data-stu-id="81650-148">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="81650-149">Cochez la case **Enable CHAP log on** .</span><span class="sxs-lookup"><span data-stu-id="81650-149">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="81650-150">Dans le champ **Nom** , tapez le nom d’utilisateur que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="81650-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="81650-151">Dans le champ **Secret de la cible** , fournissez le mot de passe que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="81650-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="81650-152">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="81650-152">Click **OK**.</span></span>
      
       ![Paramètres avancés - Généraux](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="81650-154">Dans l’onglet **Targets** de la fenêtre **iSCSI Initiator Properties**, l’état de l’appareil devrait indiquer **Connected**.</span><span class="sxs-lookup"><span data-stu-id="81650-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="81650-155">Si vous utilisez un appareil StorSimple 1200, chaque volume est monté en tant que cible iSCSI comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="81650-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="81650-156">Les étapes 3 et 4 doivent donc être répétées pour chaque volume.</span><span class="sxs-lookup"><span data-stu-id="81650-156">Hence, steps  3-4 will need to be repeated for each volume.</span></span>
   
    ![Volumes montés en tant que cibles distinctes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="81650-158">Si vous modifiez le nom iSCSI, le nouveau nom sera utilisé pour les nouvelles sessions iSCSI.</span><span class="sxs-lookup"><span data-stu-id="81650-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="81650-159">Les nouveaux paramètres ne sont pas appliqués aux sessions existantes tant que vous n’avez pas quitté puis relancé la session.</span><span class="sxs-lookup"><span data-stu-id="81650-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="81650-160">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte Windows, voir la rubrique [Considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="81650-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="81650-161">Authentification bidirectionnelle ou mutuelle</span><span class="sxs-lookup"><span data-stu-id="81650-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="81650-162">Dans l’authentification bidirectionnelle, la cible authentifie l’initiateur, puis l’initiateur authentifie la cible.</span><span class="sxs-lookup"><span data-stu-id="81650-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="81650-163">Cela oblige l’utilisateur à configurer les paramètres d’initiateur CHAP ainsi que les paramètres CHAP inverses sur l’appareil et le logiciel iSCSI Initiator sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="81650-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="81650-164">Les procédures suivantes décrivent les étapes pour configurer l’authentification mutuelle sur l’appareil et sur l’hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="81650-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="81650-165">Configuration de votre appareil pour l’authentification mutuelle</span><span class="sxs-lookup"><span data-stu-id="81650-165">To configure your device for mutual authentication</span></span>
1. <span data-ttu-id="81650-166">Dans le portail Azure Classic, sur la page **Appareils**, cliquez sur l’onglet **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="81650-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP Target](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="81650-168">Faites défiler cette page vers le bas, puis dans la section **CHAP Target** :</span><span class="sxs-lookup"><span data-stu-id="81650-168">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="81650-169">Indiquez le **nom d’utilisateur CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81650-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="81650-170">Indiquez le **mot de passe CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81650-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="81650-171">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="81650-171">Confirm the password.</span></span>
3. <span data-ttu-id="81650-172">Dans la section **CHAP Initiator** :</span><span class="sxs-lookup"><span data-stu-id="81650-172">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="81650-173">Indiquez un **nom d’utilisateur** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81650-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="81650-174">Indiquez un **mot de passe** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="81650-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="81650-175">Confirmez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="81650-175">Confirm the password.</span></span>
4. <span data-ttu-id="81650-176">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="81650-176">Click **Save**.</span></span> <span data-ttu-id="81650-177">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="81650-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="81650-178">Cliquez sur **OK** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="81650-178">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="81650-179">Configuration de l’authentification bidirectionnelle sur le serveur hôte Windows</span><span class="sxs-lookup"><span data-stu-id="81650-179">To configure bidirectional authentication on the Windows host server</span></span>
1. <span data-ttu-id="81650-180">Sur le serveur hôte Windows, démarrez l’initiateur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="81650-180">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="81650-181">Dans la fenêtre **iSCSI Initiator Properties**, cliquez sur l’onglet **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="81650-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="81650-182">Cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="81650-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="81650-183">Dans la boîte de dialogue **Secret CHAP mutuel de l’initiateur iSCSI** :</span><span class="sxs-lookup"><span data-stu-id="81650-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="81650-184">Entrez le **mot de passe CHAP inverse** que vous avez configuré dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="81650-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span></span>
   2. <span data-ttu-id="81650-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="81650-185">Click **OK**.</span></span>
      
       ![Secret CHAP mutuel de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="81650-187">Cliquez sur l’onglet **Targets** .</span><span class="sxs-lookup"><span data-stu-id="81650-187">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="81650-188">Cliquez sur le bouton **Connect** .</span><span class="sxs-lookup"><span data-stu-id="81650-188">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="81650-189">Dans la boîte de dialogue **Se connecter à la cible**, cliquez sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="81650-189">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="81650-190">Dans la boîte de dialogue **Advanced Properties** :</span><span class="sxs-lookup"><span data-stu-id="81650-190">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="81650-191">Cochez la case **Enable CHAP log on** .</span><span class="sxs-lookup"><span data-stu-id="81650-191">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="81650-192">Dans le champ **Nom** , tapez le nom d’utilisateur que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="81650-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="81650-193">Dans le champ **Secret de la cible** , fournissez le mot de passe que vous avez spécifié pour l’initiateur CHAP dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="81650-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="81650-194">Cochez la case **Perform mutual authentication** .</span><span class="sxs-lookup"><span data-stu-id="81650-194">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Paramètres avancés - Authentification mutuelle](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="81650-196">Cliquez sur **OK** pour terminer la configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="81650-196">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="81650-197">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte Windows, voir la rubrique [Considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="81650-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="81650-198">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="81650-198">Additional considerations</span></span>
<span data-ttu-id="81650-199">La fonctionnalité **Quick Connect** ne prend pas en charge les connexions pour lesquelles le protocole CHAP est activé.</span><span class="sxs-lookup"><span data-stu-id="81650-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="81650-200">Lorsque le protocole CHAP est activé, assurez-vous d’utiliser le bouton **Connect** disponible dans l’onglet **Targets** pour vous connecter à une cible.</span><span class="sxs-lookup"><span data-stu-id="81650-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Se connecter à la cible](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="81650-202">Dans la boîte de dialogue **Se connecter à la cible** qui s’affiche, cochez la case **Add this connection to the list of Favorite Targets**.</span><span class="sxs-lookup"><span data-stu-id="81650-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="81650-203">Cela garantit que chaque fois que l’ordinateur redémarre, une tentative est effectuée pour rétablir la connexion aux cibles iSCSI favorites.</span><span class="sxs-lookup"><span data-stu-id="81650-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="81650-204">Erreurs lors de la configuration</span><span class="sxs-lookup"><span data-stu-id="81650-204">Errors during configuration</span></span>
<span data-ttu-id="81650-205">Si votre configuration CHAP est incorrecte, un message d’erreur d’ **échec de l’authentification** risque d’apparaître.</span><span class="sxs-lookup"><span data-stu-id="81650-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="81650-206">Vérification de la configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="81650-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="81650-207">Vous pouvez vérifier que le protocole CHAP est utilisé en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="81650-207">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="81650-208">Vérification de votre configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="81650-208">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="81650-209">Cliquez sur **Favorite Targets**.</span><span class="sxs-lookup"><span data-stu-id="81650-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="81650-210">Sélectionnez la cible pour laquelle vous avez activé l’authentification.</span><span class="sxs-lookup"><span data-stu-id="81650-210">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="81650-211">Cliquez sur **Details**.</span><span class="sxs-lookup"><span data-stu-id="81650-211">Click **Details**.</span></span>
   
    ![Cibles favorites des propriétés de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="81650-213">Dans la boîte de dialogue **Favorite Target Details**, notez l’entrée figurant dans le champ **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="81650-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="81650-214">Si la configuration a réussi, le champ devrait afficher **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="81650-214">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Détails sur les cibles favorites](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="81650-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="81650-216">Next steps</span></span>
* <span data-ttu-id="81650-217">En savoir plus sur la [sécurité StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="81650-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="81650-218">En savoir plus sur [l’utilisation du service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="81650-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

