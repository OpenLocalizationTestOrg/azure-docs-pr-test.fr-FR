---
title: "aaaConfigure CHAP pour appareil de série StorSimple 8000 | Documents Microsoft"
description: "Décrit comment tooconfigure hello CHAP Challenge Handshake Authentication Protocol () sur un appareil StorSimple."
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
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="45636-103">Configuration de CHAP pour votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="45636-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="45636-104">Ce didacticiel explique comment tooconfigure CHAP pour votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="45636-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="45636-105">procédure de Hello détaillée dans cet article s’applique à tooStorSimple les périphériques série 8000.</span><span class="sxs-lookup"><span data-stu-id="45636-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="45636-106">CHAP est l’abréviation de Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="45636-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="45636-107">Il est un schéma d’authentification utilisé par les serveurs toovalidate hello identité des clients distants.</span><span class="sxs-lookup"><span data-stu-id="45636-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="45636-108">vérification de Hello est basée sur un mot de passe partagé ou un secret.</span><span class="sxs-lookup"><span data-stu-id="45636-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="45636-109">Le protocole CHAP peut être à sens unique (unidirectionnel) ou mutuel (bidirectionnel).</span><span class="sxs-lookup"><span data-stu-id="45636-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="45636-110">Un moyen CHAP est hello cible authentifie un initiateur.</span><span class="sxs-lookup"><span data-stu-id="45636-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="45636-111">Dans l’authentification CHAP mutuelle ou inverse, cible de hello authentifie l’initiateur de hello et puis initiateur de hello authentifie la cible de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="45636-112">L’authentification de l’initiateur peut être implémentée sans authentification cible.</span><span class="sxs-lookup"><span data-stu-id="45636-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="45636-113">Toutefois, l’authentification cible peut être implémentée uniquement si l’authentification de l’initiateur est également implémentée.</span><span class="sxs-lookup"><span data-stu-id="45636-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="45636-114">Comme meilleure pratique, nous vous recommandons de que vous utilisez la sécurité CHAP. tooenhance iSCSI.</span><span class="sxs-lookup"><span data-stu-id="45636-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="45636-115">N’oubliez pas que IPSEC n’est pas actuellement pris en charge sur les appareils StorSimple.</span><span class="sxs-lookup"><span data-stu-id="45636-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="45636-116">paramètres de CHAP de Hello sur l’appareil StorSimple hello peuvent être configurés dans hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="45636-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="45636-117">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="45636-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="45636-118">Authentification bidirectionnelle, mutuelle ou inverse</span><span class="sxs-lookup"><span data-stu-id="45636-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="45636-119">Dans chacun de ces cas, le portail hello pour appareil de hello et le logiciel initiateur iSCSI du serveur hello doit toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="45636-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="45636-120">Hello des instructions détaillées sur cette configuration sont décrites dans hello suivant le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="45636-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="45636-121">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="45636-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="45636-122">Dans une authentification unidirectionnelle, cible de hello authentifie initiateur de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="45636-123">Cette authentification nécessite de configurer les paramètres de l’initiateur CHAP hello sur l’appareil StorSimple hello et hello le logiciel initiateur iSCSI sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="45636-124">Hello des procédures détaillées pour votre appareil StorSimple et hôte Windows sont décrites ci-après.</span><span class="sxs-lookup"><span data-stu-id="45636-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="45636-125">tooconfigure votre appareil avec l’authentification unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="45636-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="45636-126">Bonjour portail Azure, accédez à service du Gestionnaire de périphériques StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="45636-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="45636-127">Cliquez sur **périphériques** et sélectionnez, puis cliquez sur un périphérique que vous souhaitez tooconfigure CHAP pour.</span><span class="sxs-lookup"><span data-stu-id="45636-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="45636-128">Accédez trop**paramètres du périphérique > sécurité**.</span><span class="sxs-lookup"><span data-stu-id="45636-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="45636-129">Bonjour **paramètres de sécurité** panneau, cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="45636-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP Initiator](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="45636-131">Bonjour **CHAP** panneau, hello et **initiateur CHAP** section :</span><span class="sxs-lookup"><span data-stu-id="45636-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="45636-132">Indiquez un nom d’utilisateur pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="45636-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="45636-133">Spécifiez un mot de passe pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="45636-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="45636-134">nom d’utilisateur CHAP Hello doit contenir 233 caractères maximum.</span><span class="sxs-lookup"><span data-stu-id="45636-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="45636-135">mot de passe CHAP Hello doit comprendre entre 12 et 16 caractères.</span><span class="sxs-lookup"><span data-stu-id="45636-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="45636-136">Un nom d’utilisateur ou le mot de passe plus long entraîne un échec d’authentification sur l’ordinateur hôte de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="45636-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="45636-137">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="45636-137">Confirm hello password.</span></span>

       ![CHAP Initiator](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="45636-139">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="45636-139">Click **Save**.</span></span> <span data-ttu-id="45636-140">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="45636-140">A confirmation message is displayed.</span></span> <span data-ttu-id="45636-141">Cliquez sur **OK** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="45636-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="45636-142">serveur hôte de l’authentification unidirectionnelle de tooconfigure sur hello Windows</span><span class="sxs-lookup"><span data-stu-id="45636-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="45636-143">Sur le serveur hôte de Windows hello, démarrez l’initiateur iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="45636-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="45636-144">Bonjour **propriétés de l’initiateur iSCSI** fenêtre, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="45636-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="45636-145">Cliquez sur hello **découverte** onglet.</span><span class="sxs-lookup"><span data-stu-id="45636-145">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI Initiator Properties](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="45636-147">Cliquez sur **Discover Portal**.</span><span class="sxs-lookup"><span data-stu-id="45636-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="45636-148">Bonjour **détecter un portail cible** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="45636-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="45636-149">Spécifier l’adresse IP de hello de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="45636-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="45636-150">Cliquez sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="45636-150">Click **Advanced**.</span></span>
      
       ![Découvrir le portail cible](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="45636-152">Bonjour **paramètres avancés** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="45636-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="45636-153">Sélectionnez hello **ouverture de session activer CHAP** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="45636-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="45636-154">Bonjour **nom** champ, le nom d’utilisateur hello approvisionnement que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="45636-155">Bonjour **secret cible** champ, alimentation hello mot de passe que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="45636-156">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="45636-156">Click **OK**.</span></span>
      
       ![Paramètres avancés - Généraux](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="45636-158">Sur hello **cibles** onglet Hello **propriétés de l’initiateur iSCSI** fenêtre, l’état du périphérique hello doit apparaître en tant que **connecté**.</span><span class="sxs-lookup"><span data-stu-id="45636-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="45636-159">Si vous utilisez un appareil StorSimple 1200, chaque volume est monté en tant que cible iSCSI.</span><span class="sxs-lookup"><span data-stu-id="45636-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="45636-160">Par conséquent, étapes 3 et 4 devez toobe répété pour chaque volume.</span><span class="sxs-lookup"><span data-stu-id="45636-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumes montés en tant que cibles distinctes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="45636-162">Si vous modifiez le nom iSCSI de hello, hello nouveau nom est utilisé pour les nouvelles sessions iSCSI.</span><span class="sxs-lookup"><span data-stu-id="45636-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="45636-163">Les nouveaux paramètres ne sont pas appliqués aux sessions existantes tant que vous n’avez pas quitté puis relancé la session.</span><span class="sxs-lookup"><span data-stu-id="45636-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="45636-164">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte de Windows hello, accédez trop[considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="45636-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="45636-165">Authentification bidirectionnelle ou mutuelle</span><span class="sxs-lookup"><span data-stu-id="45636-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="45636-166">Dans une authentification bidirectionnelle, cible de hello authentifie l’initiateur de hello et puis initiateur de hello authentifie la cible de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="45636-167">Cette procédure requiert des paramètres d’initiateur CHAP hello utilisateur tooconfigure hello, inverser les paramètres CHAP sur les appareils hello et logiciel initiateur iSCSI sur l’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="45636-168">Hello procédures suivantes décrivent l’authentification mutuelle hello étapes tooconfigure sur l’appareil de hello et sur l’ordinateur hôte de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="45636-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="45636-169">tooconfigure votre appareil pour l’authentification mutuelle</span><span class="sxs-lookup"><span data-stu-id="45636-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="45636-170">Bonjour portail Azure, accédez à service du Gestionnaire de périphériques StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="45636-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="45636-171">Cliquez sur **périphériques** et sélectionnez, puis cliquez sur un périphérique que vous souhaitez tooconfigure CHAP pour.</span><span class="sxs-lookup"><span data-stu-id="45636-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="45636-172">Accédez trop**paramètres du périphérique > sécurité**.</span><span class="sxs-lookup"><span data-stu-id="45636-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="45636-173">Bonjour **paramètres de sécurité** panneau, cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="45636-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP Target](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="45636-175">Faites défiler vers le bas sur cette page et hello **cible CHAP** section :</span><span class="sxs-lookup"><span data-stu-id="45636-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="45636-176">Indiquez le **nom d’utilisateur CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="45636-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="45636-177">Indiquez le **mot de passe CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="45636-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="45636-178">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="45636-178">Confirm hello password.</span></span>
3. <span data-ttu-id="45636-179">Bonjour **initiateur CHAP** section :</span><span class="sxs-lookup"><span data-stu-id="45636-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="45636-180">Indiquez un **nom d’utilisateur** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="45636-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="45636-181">Indiquez un **mot de passe** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="45636-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="45636-182">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="45636-182">Confirm hello password.</span></span>

       ![CHAP Initiator](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="45636-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="45636-184">Click **Save**.</span></span> <span data-ttu-id="45636-185">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="45636-185">A confirmation message is displayed.</span></span> <span data-ttu-id="45636-186">Cliquez sur **OK** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="45636-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="45636-187">serveur hôte de tooconfigure une authentification bidirectionnelle sur hello Windows</span><span class="sxs-lookup"><span data-stu-id="45636-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="45636-188">Sur le serveur hôte de Windows hello, démarrez l’initiateur iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="45636-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="45636-189">Bonjour **propriétés de l’initiateur iSCSI** fenêtre, cliquez sur hello **Configuration** onglet.</span><span class="sxs-lookup"><span data-stu-id="45636-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="45636-190">Cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="45636-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="45636-191">Bonjour **iSCSI Initiator code Secret CHAP mutuel** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="45636-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="45636-192">Hello de type **inverser un mot de passe CHAP** que vous avez configuré dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="45636-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="45636-193">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="45636-193">Click **OK**.</span></span>
      
       ![Secret CHAP mutuel de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="45636-195">Cliquez sur hello **cibles** onglet.</span><span class="sxs-lookup"><span data-stu-id="45636-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="45636-196">Cliquez sur hello **Connect** bouton.</span><span class="sxs-lookup"><span data-stu-id="45636-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="45636-197">Bonjour **connecter tooTarget** boîte de dialogue, cliquez sur **avancé**.</span><span class="sxs-lookup"><span data-stu-id="45636-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="45636-198">Bonjour **propriétés avancées** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="45636-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="45636-199">Sélectionnez hello **ouverture de session activer CHAP** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="45636-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="45636-200">Bonjour **nom** champ, le nom d’utilisateur hello approvisionnement que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="45636-201">Bonjour **secret cible** champ, alimentation hello mot de passe que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="45636-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="45636-202">Sélectionnez hello **effectuer une authentification mutuelle** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="45636-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Paramètres avancés - Authentification mutuelle](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="45636-204">Cliquez sur **OK** configuration CHAP de hello toocomplete</span><span class="sxs-lookup"><span data-stu-id="45636-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="45636-205">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte de Windows hello, accédez trop[considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="45636-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="45636-206">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="45636-206">Additional considerations</span></span>

<span data-ttu-id="45636-207">Hello **connexion rapide** fonctionnalité ne prend pas en charge les connexions pour lesquelles le protocole CHAP est activé.</span><span class="sxs-lookup"><span data-stu-id="45636-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="45636-208">Lorsque le protocole CHAP est activé, assurez-vous que vous utilisez hello **Connect** bouton est disponible sur hello **cibles** cible de tooa tooconnect onglet.</span><span class="sxs-lookup"><span data-stu-id="45636-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Se connecter tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="45636-210">Bonjour **connecter tooTarget** boîte de dialogue qui est présenté, sélectionnez hello **ajouter la liste des cibles favorites toohello connexion** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="45636-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="45636-211">Cette sélection garantit que chaque fois que hello ordinateur redémarre, une tentative est faite toorestore hello connexion toohello cibles favorites des iSCSI.</span><span class="sxs-lookup"><span data-stu-id="45636-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="45636-212">Erreurs lors de la configuration</span><span class="sxs-lookup"><span data-stu-id="45636-212">Errors during configuration</span></span>

<span data-ttu-id="45636-213">Si votre configuration CHAP est incorrecte, vous êtes probablement toosee un **Échec de l’authentification** message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="45636-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="45636-214">Vérification de la configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="45636-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="45636-215">Vous pouvez vérifier que CHAP est utilisé, hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="45636-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="45636-216">tooverify votre configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="45636-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="45636-217">Cliquez sur **Favorite Targets**.</span><span class="sxs-lookup"><span data-stu-id="45636-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="45636-218">Sélectionnez la cible de hello pour lequel vous avez activé l’authentification.</span><span class="sxs-lookup"><span data-stu-id="45636-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="45636-219">Cliquez sur **Details**.</span><span class="sxs-lookup"><span data-stu-id="45636-219">Click **Details**.</span></span>
   
    ![Cibles favorites des propriétés de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="45636-221">Bonjour **détails sur les cibles favorites** boîte de dialogue, notez hello entrée hello **authentification** champ.</span><span class="sxs-lookup"><span data-stu-id="45636-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="45636-222">Si la configuration de hello a réussi, vous devriez voir **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="45636-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Détails sur les cibles favorites](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="45636-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45636-224">Next steps</span></span>

* <span data-ttu-id="45636-225">En savoir plus sur la [sécurité StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="45636-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="45636-226">En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="45636-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

