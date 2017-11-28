---
title: "Enregistrer un ticket de support pour la gamme StorSimple 8000 | Microsoft Docs"
description: "Découvrez comment créer une demande de support et démarrer une session de support sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="68061-103">Contactez le support technique Microsoft pour votre système StorSimple</span><span class="sxs-lookup"><span data-stu-id="68061-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="68061-104">Si vous rencontrez des problèmes avec votre solution Microsoft Azure StorSimple, vous pouvez créer une demande de service pour le support technique.</span><span class="sxs-lookup"><span data-stu-id="68061-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="68061-105">Lors d’une session en ligne avec votre ingénieur de support, vous devrez également démarrer une session de support sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68061-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="68061-106">Cet article vous guide tout au long des procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="68061-106">This article walks you through:</span></span>

* <span data-ttu-id="68061-107">Création d’une demande de support</span><span class="sxs-lookup"><span data-stu-id="68061-107">How to create a support request.</span></span>
* <span data-ttu-id="68061-108">Démarrage d’une session de support dans l’interface Windows PowerShell de votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="68061-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="68061-109">Examinez les [informations et les contrats de niveau de service relatifs à la prise en charge de la gamme StorSimple 8000](https://msdn.microsoft.com/library/mt433077.aspx) avant de créer une demande de support.</span><span class="sxs-lookup"><span data-stu-id="68061-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="68061-110">Création d’une demande de support</span><span class="sxs-lookup"><span data-stu-id="68061-110">Create a support request</span></span>
<span data-ttu-id="68061-111">Procédez comme suit pour créer une demande de support.</span><span class="sxs-lookup"><span data-stu-id="68061-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="68061-112">Création d’une demande de support</span><span class="sxs-lookup"><span data-stu-id="68061-112">To create a support request</span></span>
1. <span data-ttu-id="68061-113">Sur le [portail Azure Classic](https://manage.windowsazure.com/), dans le coin supérieur droit, cliquez sur votre nom de compte, puis sur **Contacter le support Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="68061-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Contacter le support MS via le Portail de gestion](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="68061-115">Vous êtes redirigé vers le nouveau portail Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68061-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="68061-116">Cliquez sur la mosaïque **Nouvelle demande de support** .</span><span class="sxs-lookup"><span data-stu-id="68061-116">Click the **New support request** tile.</span></span>
   
    ![Contacter le support MS avec le nouveau portail](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="68061-118">Sur le côté droit de l'écran, le volet **Nouvelle demande de support** s'affiche.</span><span class="sxs-lookup"><span data-stu-id="68061-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![Volet Nouvelle demande de support](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="68061-120">Dans la boîte de dialogue **Bases** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68061-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="68061-121">Dans la liste déroulante **Type de problème**, sélectionnez **Technique**.</span><span class="sxs-lookup"><span data-stu-id="68061-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="68061-122">Sélectionnez un **Abonnement** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="68061-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="68061-123">Dans la liste déroulante **Service**, sélectionnez **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="68061-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="68061-124">Sélectionnez un **Plan de support** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="68061-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="68061-125">Vous avez besoin d'un plan de support payant pour bénéficier du support technique.</span><span class="sxs-lookup"><span data-stu-id="68061-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="68061-126">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="68061-126">Click **Next**.</span></span> <span data-ttu-id="68061-127">La boîte de dialogue **Problème** s'affiche.</span><span class="sxs-lookup"><span data-stu-id="68061-127">The **Problem** dialog box appears.</span></span>
   
    ![Volet Nouvelle demande de support](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="68061-129">Dans la boîte de dialogue **Problème** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68061-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="68061-130">Sélectionnez un niveau de **Gravité** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="68061-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="68061-131">Sélectionnez un **Type de problème** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="68061-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="68061-132">Sélectionnez une **Catégorie** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="68061-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="68061-133">Dans la zone **Détails** , décrivez en quelques mots votre problème.</span><span class="sxs-lookup"><span data-stu-id="68061-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="68061-134">Dans la zone **Date** , indiquez la date, l’heure et le fuseau horaire correspondant à la dernière occurrence de votre problème.</span><span class="sxs-lookup"><span data-stu-id="68061-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="68061-135">Sous **Téléchargement du fichier**, cliquez sur l'icône du dossier pour accéder à votre package de support.</span><span class="sxs-lookup"><span data-stu-id="68061-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="68061-136">Cochez la case **Partager les informations de diagnostic** .</span><span class="sxs-lookup"><span data-stu-id="68061-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="68061-137">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="68061-137">Click **Next**.</span></span> <span data-ttu-id="68061-138">La boîte de dialogue **Coordonnées** s'affiche.</span><span class="sxs-lookup"><span data-stu-id="68061-138">The **Contact information** dialog box appears.</span></span>
   
    ![Volet Nouvelle demande de support](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="68061-140">Entrez vos informations de contact et sélectionnez une méthode de contact (téléphone ou courrier électronique).</span><span class="sxs-lookup"><span data-stu-id="68061-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="68061-141">Cochez la case **Enregistrer les modifications de contact pour les futures demandes de support** .</span><span class="sxs-lookup"><span data-stu-id="68061-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="68061-142">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="68061-142">Click **Create**.</span></span>

<span data-ttu-id="68061-143">Une fois votre demande envoyée, un ingénieur de support vous contactera dès que possible pour traiter votre demande.</span><span class="sxs-lookup"><span data-stu-id="68061-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="68061-144">Démarrage d’une session de support dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="68061-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="68061-145">Pour résoudre les problèmes que vous pouvez rencontrer avec l’appareil StorSimple, vous devrez contacter l'équipe de Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="68061-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="68061-146">Le support Microsoft devra peut-être utiliser une session de support pour se connecter à votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68061-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="68061-147">Procédez comme suit pour démarrer une session de support :</span><span class="sxs-lookup"><span data-stu-id="68061-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="68061-148">Démarrage d’une session de support</span><span class="sxs-lookup"><span data-stu-id="68061-148">To start a support session</span></span>
1. <span data-ttu-id="68061-149">Accédez directement à l’appareil à l'aide de la console série ou via une session telnet à partir d'un ordinateur distant.</span><span class="sxs-lookup"><span data-stu-id="68061-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="68061-150">Pour cela, suivez les étapes de la section [Utilisation de PuTTY pour se connecter à la console série de l’appareil](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="68061-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="68061-151">Dans la session qui s’ouvre, appuyez sur la touche **Entrée** pour afficher une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="68061-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="68061-152">Dans le menu de la console série, sélectionnez l’option 1, **Ouvrir une session avec un accès total**.</span><span class="sxs-lookup"><span data-stu-id="68061-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="68061-153">À l'invite de commande, entrez le mot de passe suivant :</span><span class="sxs-lookup"><span data-stu-id="68061-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="68061-154">À l'invite de commande, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="68061-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="68061-155">Une chaîne chiffrée s'affiche.</span><span class="sxs-lookup"><span data-stu-id="68061-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="68061-156">Copiez cette chaîne dans un éditeur de texte comme le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="68061-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="68061-157">Enregistrez cette chaîne et envoyez-la par e-mail au support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="68061-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="68061-158">Vous pouvez désactiver l’accès au support en exécutant `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="68061-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="68061-159">L’appareil StorSimple tentera également de désactiver l'accès au support 8 heures après le début de la session.</span><span class="sxs-lookup"><span data-stu-id="68061-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="68061-160">Il est recommandé de modifier vos informations d'identification de l’appareil StorSimple après le lancement d'une session de support.</span><span class="sxs-lookup"><span data-stu-id="68061-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

