---
title: "aaaConfigure CHAP pour appareil de série StorSimple 8000 | Documents Microsoft"
description: "Décrit comment tooconfigure hello CHAP Challenge Handshake Authentication Protocol () sur un appareil StorSimple."
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
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="70597-103">Configuration de CHAP pour votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="70597-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="70597-104">Ce didacticiel explique comment tooconfigure CHAP pour votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="70597-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="70597-105">procédure de Hello détaillée dans cet article s’applique tooStorSimple 8000 series, ainsi que les appareils StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="70597-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="70597-106">CHAP est l’abréviation de Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="70597-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="70597-107">Il est un schéma d’authentification utilisé par les serveurs toovalidate hello identité des clients distants.</span><span class="sxs-lookup"><span data-stu-id="70597-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="70597-108">vérification de Hello est basée sur un mot de passe partagé ou un secret.</span><span class="sxs-lookup"><span data-stu-id="70597-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="70597-109">Le protocole CHAP peut être à sens unique (unidirectionnel) ou mutuel (bidirectionnel).</span><span class="sxs-lookup"><span data-stu-id="70597-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="70597-110">Authentification CHAP unidirectionnelle est lorsque hello cible authentifie un initiateur.</span><span class="sxs-lookup"><span data-stu-id="70597-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="70597-111">Authentification CHAP mutuelle ou inverse, sur hello autre part, requiert que la cible de hello authentifier l’initiateur de hello et puis hello initiateur doit authentifier hello cible.</span><span class="sxs-lookup"><span data-stu-id="70597-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="70597-112">L’authentification de l’initiateur peut être implémentée sans authentification cible.</span><span class="sxs-lookup"><span data-stu-id="70597-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="70597-113">Toutefois, l’authentification cible peut être implémentée uniquement si l’authentification de l’initiateur est également implémentée.</span><span class="sxs-lookup"><span data-stu-id="70597-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="70597-114">Comme meilleure pratique, nous vous recommandons de que vous utilisez la sécurité CHAP. tooenhance iSCSI.</span><span class="sxs-lookup"><span data-stu-id="70597-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="70597-115">N’oubliez pas que IPSEC n’est pas actuellement pris en charge sur les appareils StorSimple.</span><span class="sxs-lookup"><span data-stu-id="70597-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="70597-116">paramètres de CHAP de Hello sur l’appareil StorSimple hello peuvent être configurés dans hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="70597-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="70597-117">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="70597-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="70597-118">Authentification bidirectionnelle, mutuelle ou inverse</span><span class="sxs-lookup"><span data-stu-id="70597-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="70597-119">Dans chacun de ces cas, le portail hello pour appareil de hello et le logiciel initiateur iSCSI du serveur hello doit toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="70597-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="70597-120">Hello des instructions détaillées sur cette configuration sont décrites dans hello suivant le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="70597-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="70597-121">Authentification unidirectionnelle ou unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="70597-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="70597-122">Dans une authentification unidirectionnelle, cible de hello authentifie initiateur de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="70597-123">Cette authentification nécessite de configurer les paramètres de l’initiateur CHAP hello sur l’appareil StorSimple hello et hello le logiciel initiateur iSCSI sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="70597-124">Hello des procédures détaillées pour votre appareil StorSimple et hôte Windows sont décrites ci-après.</span><span class="sxs-lookup"><span data-stu-id="70597-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="70597-125">tooconfigure votre appareil avec l’authentification unidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="70597-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="70597-126">Bonjour portail Azure classic sur hello **périphériques** , cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="70597-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP Initiator](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="70597-128">Faites défiler vers le bas sur cette page et hello **initiateur CHAP** section :</span><span class="sxs-lookup"><span data-stu-id="70597-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="70597-129">Indiquez un nom d’utilisateur pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="70597-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="70597-130">Spécifiez un mot de passe pour votre initiateur CHAP.</span><span class="sxs-lookup"><span data-stu-id="70597-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="70597-131">nom d’utilisateur CHAP Hello doit contenir 233 caractères maximum.</span><span class="sxs-lookup"><span data-stu-id="70597-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="70597-132">mot de passe CHAP Hello doit comprendre entre 12 et 16 caractères.</span><span class="sxs-lookup"><span data-stu-id="70597-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="70597-133">Un nom d’utilisateur ou le mot de passe plus long entraîne un échec d’authentification sur l’ordinateur hôte de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="70597-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="70597-134">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="70597-134">Confirm hello password.</span></span>
3. <span data-ttu-id="70597-135">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="70597-135">Click **Save**.</span></span> <span data-ttu-id="70597-136">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="70597-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="70597-137">Cliquez sur **OK** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="70597-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="70597-138">serveur hôte de l’authentification unidirectionnelle de tooconfigure sur hello Windows</span><span class="sxs-lookup"><span data-stu-id="70597-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="70597-139">Sur le serveur hôte de Windows hello, démarrez l’initiateur iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="70597-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="70597-140">Bonjour **propriétés de l’initiateur iSCSI** fenêtre, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="70597-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="70597-141">Cliquez sur hello **découverte** onglet.</span><span class="sxs-lookup"><span data-stu-id="70597-141">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI Initiator Properties](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="70597-143">Cliquez sur **Discover Portal**.</span><span class="sxs-lookup"><span data-stu-id="70597-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="70597-144">Bonjour **détecter un portail cible** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="70597-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="70597-145">Spécifier l’adresse IP de hello de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="70597-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="70597-146">Cliquez sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="70597-146">Click **Advanced**.</span></span>
      
       ![Découvrir le portail cible](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="70597-148">Bonjour **paramètres avancés** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="70597-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="70597-149">Sélectionnez hello **ouverture de session activer CHAP** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="70597-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="70597-150">Bonjour **nom** champ, le nom d’utilisateur hello approvisionnement que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="70597-151">Bonjour **secret cible** champ, alimentation hello mot de passe que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="70597-152">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="70597-152">Click **OK**.</span></span>
      
       ![Paramètres avancés - Généraux](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="70597-154">Sur hello **cibles** onglet Hello **propriétés de l’initiateur iSCSI** fenêtre, l’état du périphérique hello doit apparaître en tant que **connecté**.</span><span class="sxs-lookup"><span data-stu-id="70597-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="70597-155">Si vous utilisez un appareil StorSimple 1200, chaque volume est monté en tant que cible iSCSI comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="70597-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="70597-156">Par conséquent, étapes 3 et 4 devez toobe répété pour chaque volume.</span><span class="sxs-lookup"><span data-stu-id="70597-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumes montés en tant que cibles distinctes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="70597-158">Si vous modifiez le nom iSCSI de hello, nouveau nom de hello sera utilisé pour les nouvelles sessions iSCSI.</span><span class="sxs-lookup"><span data-stu-id="70597-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="70597-159">Les nouveaux paramètres ne sont pas appliqués aux sessions existantes tant que vous n’avez pas quitté puis relancé la session.</span><span class="sxs-lookup"><span data-stu-id="70597-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="70597-160">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte de Windows hello, accédez trop[considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="70597-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="70597-161">Authentification bidirectionnelle ou mutuelle</span><span class="sxs-lookup"><span data-stu-id="70597-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="70597-162">Dans une authentification bidirectionnelle, cible de hello authentifie l’initiateur de hello et puis initiateur de hello authentifie la cible de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="70597-163">Cela nécessite de paramètres de l’initiateur hello utilisateur tooconfigure hello CHAP, ainsi que hello inverse les paramètres CHAP sur l’appareil de hello et le logiciel initiateur iSCSI sur l’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="70597-164">Hello procédures suivantes décrivent l’authentification mutuelle hello étapes tooconfigure sur l’appareil de hello et sur l’ordinateur hôte de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="70597-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="70597-165">tooconfigure votre appareil pour l’authentification mutuelle</span><span class="sxs-lookup"><span data-stu-id="70597-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="70597-166">Bonjour portail Azure classic sur hello **périphériques** , cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="70597-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP Target](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="70597-168">Faites défiler vers le bas sur cette page et hello **cible CHAP** section :</span><span class="sxs-lookup"><span data-stu-id="70597-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="70597-169">Indiquez le **nom d’utilisateur CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="70597-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="70597-170">Indiquez le **mot de passe CHAP inverse** de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="70597-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="70597-171">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="70597-171">Confirm hello password.</span></span>
3. <span data-ttu-id="70597-172">Bonjour **initiateur CHAP** section :</span><span class="sxs-lookup"><span data-stu-id="70597-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="70597-173">Indiquez un **nom d’utilisateur** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="70597-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="70597-174">Indiquez un **mot de passe** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="70597-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="70597-175">Confirmer le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="70597-175">Confirm hello password.</span></span>
4. <span data-ttu-id="70597-176">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="70597-176">Click **Save**.</span></span> <span data-ttu-id="70597-177">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="70597-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="70597-178">Cliquez sur **OK** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="70597-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="70597-179">serveur hôte de tooconfigure une authentification bidirectionnelle sur hello Windows</span><span class="sxs-lookup"><span data-stu-id="70597-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="70597-180">Sur le serveur hôte de Windows hello, démarrez l’initiateur iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="70597-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="70597-181">Bonjour **propriétés de l’initiateur iSCSI** fenêtre, cliquez sur hello **Configuration** onglet.</span><span class="sxs-lookup"><span data-stu-id="70597-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="70597-182">Cliquez sur **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="70597-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="70597-183">Bonjour **iSCSI Initiator code Secret CHAP mutuel** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="70597-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="70597-184">Hello de type **inverser un mot de passe CHAP** que vous avez configuré dans hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="70597-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="70597-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="70597-185">Click **OK**.</span></span>
      
       ![Secret CHAP mutuel de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="70597-187">Cliquez sur hello **cibles** onglet.</span><span class="sxs-lookup"><span data-stu-id="70597-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="70597-188">Cliquez sur hello **Connect** bouton.</span><span class="sxs-lookup"><span data-stu-id="70597-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="70597-189">Bonjour **connecter tooTarget** boîte de dialogue, cliquez sur **avancé**.</span><span class="sxs-lookup"><span data-stu-id="70597-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="70597-190">Bonjour **propriétés avancées** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="70597-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="70597-191">Sélectionnez hello **ouverture de session activer CHAP** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="70597-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="70597-192">Bonjour **nom** champ, le nom d’utilisateur hello approvisionnement que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="70597-193">Bonjour **secret cible** champ, alimentation hello mot de passe que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="70597-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="70597-194">Sélectionnez hello **effectuer une authentification mutuelle** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="70597-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Paramètres avancés - Authentification mutuelle](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="70597-196">Cliquez sur **OK** configuration CHAP de hello toocomplete</span><span class="sxs-lookup"><span data-stu-id="70597-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="70597-197">Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte de Windows hello, accédez trop[considérations supplémentaires](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="70597-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="70597-198">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="70597-198">Additional considerations</span></span>
<span data-ttu-id="70597-199">Hello **connexion rapide** fonctionnalité ne prend pas en charge les connexions pour lesquelles le protocole CHAP est activé.</span><span class="sxs-lookup"><span data-stu-id="70597-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="70597-200">Lorsque le protocole CHAP est activé, assurez-vous que vous utilisez hello **Connect** bouton est disponible sur hello **cibles** cible de tooa tooconnect onglet.</span><span class="sxs-lookup"><span data-stu-id="70597-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Se connecter tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="70597-202">Bonjour **connecter tooTarget** boîte de dialogue qui est présenté, sélectionnez hello **ajouter la liste des cibles favorites toohello connexion** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="70597-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="70597-203">Cela garantit que chaque fois que hello ordinateur redémarre, une tentative est faite toorestore hello connexion toohello cibles favorites des iSCSI.</span><span class="sxs-lookup"><span data-stu-id="70597-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="70597-204">Erreurs lors de la configuration</span><span class="sxs-lookup"><span data-stu-id="70597-204">Errors during configuration</span></span>
<span data-ttu-id="70597-205">Si votre configuration CHAP est incorrecte, vous êtes probablement toosee un **Échec de l’authentification** message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="70597-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="70597-206">Vérification de la configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="70597-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="70597-207">Vous pouvez vérifier que CHAP est utilisé, hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="70597-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="70597-208">tooverify votre configuration CHAP</span><span class="sxs-lookup"><span data-stu-id="70597-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="70597-209">Cliquez sur **Favorite Targets**.</span><span class="sxs-lookup"><span data-stu-id="70597-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="70597-210">Sélectionnez la cible de hello pour lequel vous avez activé l’authentification.</span><span class="sxs-lookup"><span data-stu-id="70597-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="70597-211">Cliquez sur **Details**.</span><span class="sxs-lookup"><span data-stu-id="70597-211">Click **Details**.</span></span>
   
    ![Cibles favorites des propriétés de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="70597-213">Bonjour **détails sur les cibles favorites** boîte de dialogue, notez hello entrée hello **authentification** champ.</span><span class="sxs-lookup"><span data-stu-id="70597-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="70597-214">Si la configuration de hello a réussi, vous devriez voir **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="70597-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Détails sur les cibles favorites](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="70597-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70597-216">Next steps</span></span>
* <span data-ttu-id="70597-217">En savoir plus sur la [sécurité StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="70597-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="70597-218">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="70597-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

