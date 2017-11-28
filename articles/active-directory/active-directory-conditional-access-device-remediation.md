---
title: "aaaYou ne peut pas y accéder à partir de maintenant hello portail Azure à partir d’un appareil Windows | Documents Microsoft"
description: "En savoir où vous ne pouvez pas get il à partir d’ici provient et ce que vous pourriez vérifier tooavoid en cours d’exécution dans cette boîte de dialogue."
services: active-directory
keywords: "accès conditionnel en fonction de l’appareil, inscription de l’appareil, activer l’inscription de l’appareil, inscription de l’appareil et GPM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="1ff65-104">Problèmes d’accès aux ressources sur un appareil Windows</span><span class="sxs-lookup"><span data-stu-id="1ff65-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="1ff65-105">Par exemple, lors d’une tentative d’accès à l’intranet SharePoint Online de votre organisation, vous pouvez rencontrer une page indiquant que *vous ne pouvez pas y accéder à partir de votre emplacement*.</span><span class="sxs-lookup"><span data-stu-id="1ff65-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="1ff65-106">Vous voyez cette page, car votre administrateur a configuré une stratégie d’accès conditionnel qui empêche les ressources de l’organisation accès tooyour sous certaines conditions.</span><span class="sxs-lookup"><span data-stu-id="1ff65-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="1ff65-107">Bien qu’il soit nécessaire toocontact technique ou votre tooget administrateur résoudre ce problème, il existe quelques éléments, que vous pouvez essayer par vous-même, tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="1ff65-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="1ff65-108">Si vous utilisez un **Windows** appareil, vous devez vérifier hello suivant :</span><span class="sxs-lookup"><span data-stu-id="1ff65-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="1ff65-109">Le navigateur que vous utilisez est-il pris en charge ?</span><span class="sxs-lookup"><span data-stu-id="1ff65-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="1ff65-110">Votre appareil exécute-t-il une version prise en charge de Windows ?</span><span class="sxs-lookup"><span data-stu-id="1ff65-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="1ff65-111">Votre appareil est-il conforme ?</span><span class="sxs-lookup"><span data-stu-id="1ff65-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="1ff65-112">Navigateur pris en charge</span><span class="sxs-lookup"><span data-stu-id="1ff65-112">Supported browser</span></span>

<span data-ttu-id="1ff65-113">Si votre administrateur a configuré une stratégie d’accès conditionnel, vous pouvez uniquement accéder aux ressources de votre organisation à l’aide d’un navigateur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1ff65-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="1ff65-114">Sur un appareil Windows, seuls **Internet Explorer** et **Edge** sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1ff65-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="1ff65-115">Vous pouvez facilement identifier si vous ne peut pas accéder à une ressource en raison de navigateur non pris en charge de tooan en consultant la section des détails de la page d’erreur hello hello :</span><span class="sxs-lookup"><span data-stu-id="1ff65-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="1ff65-116">![Messages d’accès refusé aux navigateurs non pris en charge](./media/active-directory-conditional-access-device-remediation/02.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="1ff65-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="1ff65-117">mise à jour de la seule Hello est toouse un navigateur qui prend en charge de l’application hello pour votre plateforme d’appareils.</span><span class="sxs-lookup"><span data-stu-id="1ff65-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="1ff65-118">Pour obtenir une liste complète des navigateurs pris en charge, consultez la liste des [navigateurs pris en charge](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="1ff65-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="1ff65-119">Versions de Windows prises en charge</span><span class="sxs-lookup"><span data-stu-id="1ff65-119">Supported versions of Windows</span></span>

<span data-ttu-id="1ff65-120">suivant de Hello doit être remplies sur le système de d’exploitation Windows hello sur votre appareil :</span><span class="sxs-lookup"><span data-stu-id="1ff65-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="1ff65-121">Si vous exécutez un système d’exploitation Windows sur votre appareil, il doit toobe Windows 7 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1ff65-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="1ff65-122">Si vous exécutez un système d’exploitation Windows sur votre appareil, il doit toobe Windows Server 2008 R2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1ff65-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="1ff65-123">Conformité de l’appareil</span><span class="sxs-lookup"><span data-stu-id="1ff65-123">Compliant device</span></span>

<span data-ttu-id="1ff65-124">Votre administrateur peut avoir configuré une stratégie d’accès conditionnel qui permet aux ressources de l’organisation de tooyour accès uniquement à partir d’appareils conformes.</span><span class="sxs-lookup"><span data-stu-id="1ff65-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="1ff65-125">Active Directory local toobe conforme, que votre appareil doit être soit joint tooyour ou joint tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ff65-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="1ff65-126">Vous pouvez facilement identifier si vous ne pouvez pas accéder à une ressource en raison de l’appareil tooa qui n’est pas conforme en examinant la section des détails de la page d’erreur hello hello :</span><span class="sxs-lookup"><span data-stu-id="1ff65-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="1ff65-127">![Messages d’accès refusé aux appareils non enregistrés](./media/active-directory-conditional-access-device-remediation/01.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="1ff65-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="1ff65-128">Est votre tooan appareil joint sur le site Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1ff65-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="1ff65-129">**Si votre appareil est joint tooan locale Active Directory dans votre organisation :**</span><span class="sxs-lookup"><span data-stu-id="1ff65-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="1ff65-130">Assurez-vous que vous vous connectez tooWindows à l’aide de votre compte professionnel (votre compte Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1ff65-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="1ff65-131">Se connecter tooyour de réseau d’entreprise via un réseau privé virtuel (VPN) ou un DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="1ff65-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="1ff65-132">Une fois que vous êtes connecté, appuyez sur touche du logo Windows hello + toolock de clé hello L votre session Windows.</span><span class="sxs-lookup"><span data-stu-id="1ff65-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="1ff65-133">Déverrouillez votre session Windows en saisissant les informations d’identification de votre compte de travail.</span><span class="sxs-lookup"><span data-stu-id="1ff65-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="1ff65-134">Patientez une minute et réessayez tooaccess hello application ou service.</span><span class="sxs-lookup"><span data-stu-id="1ff65-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="1ff65-135">Si vous voyez hello même page, cliquez sur hello **plus de détails** lier, puis contactez votre administrateur avec des détails de hello.</span><span class="sxs-lookup"><span data-stu-id="1ff65-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="1ff65-136">Est votre tooan appareil ne joint pas sur le site Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1ff65-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="1ff65-137">Si votre appareil n’est pas joint tooan Active Directory local et exécute Windows 10, vous avez deux options :</span><span class="sxs-lookup"><span data-stu-id="1ff65-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="1ff65-138">Exécuter Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="1ff65-138">Run Azure AD Join</span></span>
* <span data-ttu-id="1ff65-139">Ajouter votre travail ou d’établissement scolaire tooWindows de compte</span><span class="sxs-lookup"><span data-stu-id="1ff65-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="1ff65-140">Pour plus d’informations sur les différences entre ces options, consultez la section [Utilisation d’appareils Windows 10 sur votre lieu de travail](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="1ff65-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="1ff65-141">Ainsi :</span><span class="sxs-lookup"><span data-stu-id="1ff65-141">If your device:</span></span>

- <span data-ttu-id="1ff65-142">Appartient tooyour organisation, vous devez exécuter Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="1ff65-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="1ff65-143">Est un périphérique personnel ou un appareil Windows phone, vous devez ajouter votre travail ou scolaire tooWindows de compte</span><span class="sxs-lookup"><span data-stu-id="1ff65-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="1ff65-144">Exécution de l’option Azure AD Join sur Windows 10</span><span class="sxs-lookup"><span data-stu-id="1ff65-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="1ff65-145">Hello toojoin étapes votre tooAzure DISPOSITIF AD sont liés version hello de Windows 10 en cours d’exécution sur ce dernier.</span><span class="sxs-lookup"><span data-stu-id="1ff65-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="1ff65-146">version de hello toodetermine de votre système d’exploitation Windows 10, exécutez hello **winver** commande :</span><span class="sxs-lookup"><span data-stu-id="1ff65-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Version de Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="1ff65-148">**Mise à jour anniversaire Windows 10 (version 1607) :**</span><span class="sxs-lookup"><span data-stu-id="1ff65-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="1ff65-149">Ouvrez hello **paramètres** application.</span><span class="sxs-lookup"><span data-stu-id="1ff65-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1ff65-150">Cliquez sur **Comptes** > **Access work or school** (Accès professionnel ou scolaire).</span><span class="sxs-lookup"><span data-stu-id="1ff65-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="1ff65-151">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-151">Click **Connect**.</span></span>
4. <span data-ttu-id="1ff65-152">Cliquez sur **joindre cette tooAzure appareil AD**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="1ff65-153">Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.</span><span class="sxs-lookup"><span data-stu-id="1ff65-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="1ff65-154">Déconnectez-vous puis reconnectez-vous à l’aide de votre compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="1ff65-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="1ff65-155">Essayez à nouveau l’application de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="1ff65-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="1ff65-156">**Mise à jour Windows 10 de novembre 2015 (version 1511) :**</span><span class="sxs-lookup"><span data-stu-id="1ff65-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="1ff65-157">Ouvrez hello **paramètres** application.</span><span class="sxs-lookup"><span data-stu-id="1ff65-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1ff65-158">Cliquez sur **Système** > **À propos de**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="1ff65-159">Cliquez sur **Joindre Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="1ff65-160">Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.</span><span class="sxs-lookup"><span data-stu-id="1ff65-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1ff65-161">Déconnectez-vous et reconnectez-vous à l’aide de votre compte professionnel (votre compte Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ff65-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="1ff65-162">Essayez à nouveau l’application de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="1ff65-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="1ff65-163">Workplace Join pour Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="1ff65-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="1ff65-164">Si votre appareil n’est pas joint au domaine et exécutant Windows 8.1, toodo une jonction et s’inscrire à Microsoft Intune, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ff65-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="1ff65-165">Ouvrez **Paramètres du PC**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="1ff65-166">Cliquez sur **Réseau** > **Espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="1ff65-167">Cliquez sur **Joindre**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-167">Click **Join**.</span></span>
4. <span data-ttu-id="1ff65-168">Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.</span><span class="sxs-lookup"><span data-stu-id="1ff65-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1ff65-169">Cliquez sur **Activer**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="1ff65-170">Essayez à nouveau l’application de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="1ff65-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="1ff65-171">Ajouter votre travail ou d’établissement scolaire tooWindows de compte</span><span class="sxs-lookup"><span data-stu-id="1ff65-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="1ff65-172">**Mise à jour anniversaire Windows 10 (version 1607) :**</span><span class="sxs-lookup"><span data-stu-id="1ff65-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="1ff65-173">Ouvrez hello **paramètres** application.</span><span class="sxs-lookup"><span data-stu-id="1ff65-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1ff65-174">Cliquez sur **Comptes** > **Access work or school** (Accès professionnel ou scolaire).</span><span class="sxs-lookup"><span data-stu-id="1ff65-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="1ff65-175">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-175">Click **Connect**.</span></span>
4. <span data-ttu-id="1ff65-176">Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.</span><span class="sxs-lookup"><span data-stu-id="1ff65-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1ff65-177">Essayez à nouveau l’application de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="1ff65-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="1ff65-178">**Mise à jour Windows 10 de novembre 2015 (version 1511) :**</span><span class="sxs-lookup"><span data-stu-id="1ff65-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="1ff65-179">Ouvrez hello **paramètres** application.</span><span class="sxs-lookup"><span data-stu-id="1ff65-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1ff65-180">Cliquez sur **Comptes** > **Vos comptes**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="1ff65-181">Cliquez sur **Ajouter un compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="1ff65-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="1ff65-182">Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.</span><span class="sxs-lookup"><span data-stu-id="1ff65-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1ff65-183">Essayez à nouveau l’application de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="1ff65-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="1ff65-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ff65-184">Next steps</span></span>
[<span data-ttu-id="1ff65-185">Accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ff65-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

