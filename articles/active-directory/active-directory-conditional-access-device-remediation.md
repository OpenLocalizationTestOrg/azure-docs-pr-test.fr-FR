---
title: "Résolution des problèmes d’accès aux ressources sur le portail Azure depuis un appareil Windows | Microsoft Docs"
description: "Découvrez d’où proviennent les problèmes d’accès et quels éléments vérifier pour éviter de rencontrer cette boîte de dialogue."
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
ms.openlocfilehash: 16543c7bb7b6b236dcc24093c9963bc218ca1fa6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="36810-104">Problèmes d’accès aux ressources sur un appareil Windows</span><span class="sxs-lookup"><span data-stu-id="36810-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="36810-105">Par exemple, lors d’une tentative d’accès à l’intranet SharePoint Online de votre organisation, vous pouvez rencontrer une page indiquant que *vous ne pouvez pas y accéder à partir de votre emplacement*.</span><span class="sxs-lookup"><span data-stu-id="36810-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="36810-106">Or, cette page s’affiche parce que votre administrateur a configuré une stratégie d’accès conditionnel, qui empêche l’accès aux ressources de votre organisation sous certaines conditions.</span><span class="sxs-lookup"><span data-stu-id="36810-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access to your organization's resources under certain conditions.</span></span> <span data-ttu-id="36810-107">Il peut être nécessaire de contacter le support technique ou votre administrateur pour résoudre ce problème. Toutefois, vous pouvez d’abord essayer de le faire vous-même.</span><span class="sxs-lookup"><span data-stu-id="36810-107">While it might be necessary to contact helpdesk or your administrator to get this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="36810-108">Si vous utilisez un appareil **Windows**, vérifiez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="36810-108">If you are using a **Windows** device, you should check the following:</span></span>

- <span data-ttu-id="36810-109">Le navigateur que vous utilisez est-il pris en charge ?</span><span class="sxs-lookup"><span data-stu-id="36810-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="36810-110">Votre appareil exécute-t-il une version prise en charge de Windows ?</span><span class="sxs-lookup"><span data-stu-id="36810-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="36810-111">Votre appareil est-il conforme ?</span><span class="sxs-lookup"><span data-stu-id="36810-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="36810-112">Navigateur pris en charge</span><span class="sxs-lookup"><span data-stu-id="36810-112">Supported browser</span></span>

<span data-ttu-id="36810-113">Si votre administrateur a configuré une stratégie d’accès conditionnel, vous pouvez uniquement accéder aux ressources de votre organisation à l’aide d’un navigateur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="36810-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="36810-114">Sur un appareil Windows, seuls **Internet Explorer** et **Edge** sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="36810-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="36810-115">Vous pouvez facilement savoir si le fait que vous ne puissiez pas accéder à une ressource est lié à l’utilisation d’un navigateur non pris en charge, en consultant la section des détails de la page d’erreur :</span><span class="sxs-lookup"><span data-stu-id="36810-115">You can easily identify whether you can't access a resource due to an unsupported browser by looking at the details section of the error page:</span></span>

<span data-ttu-id="36810-116">![Messages d’accès refusé aux navigateurs non pris en charge](./media/active-directory-conditional-access-device-remediation/02.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="36810-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="36810-117">La seule possibilité consiste à utiliser un navigateur pris en charge par l’application sur la plateforme de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="36810-117">The only remediation is to use a browser that the application supports for your device platform.</span></span> <span data-ttu-id="36810-118">Pour obtenir une liste complète des navigateurs pris en charge, consultez la liste des [navigateurs pris en charge](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="36810-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="36810-119">Versions de Windows prises en charge</span><span class="sxs-lookup"><span data-stu-id="36810-119">Supported versions of Windows</span></span>

<span data-ttu-id="36810-120">Les conditions suivantes doivent exister sur le système d’exploitation Windows de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="36810-120">The following must be true about the Windows operating system on your device:</span></span> 

- <span data-ttu-id="36810-121">Si vous exécutez un système d’exploitation Windows sur votre appareil, il doit s’agir de Windows 7 ou d’une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="36810-121">If you are running a Windows desktop operating system on your device, it needs to be Windows 7 or later.</span></span>
- <span data-ttu-id="36810-122">Si vous exécutez un système d’exploitation Windows sur votre appareil, il doit s’agir de Windows Server 2008 R2 ou d’une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="36810-122">If you are running a Windows server operating system on your device, it needs to be Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="36810-123">Conformité de l’appareil</span><span class="sxs-lookup"><span data-stu-id="36810-123">Compliant device</span></span>

<span data-ttu-id="36810-124">Il se peut que l’administrateur ait configuré une stratégie d’accès conditionnel qui restreint l’accès aux ressources de l’organisation aux seuls appareils conformes.</span><span class="sxs-lookup"><span data-stu-id="36810-124">Your administrator might have configured a conditional access policy that allows access to your organization's resources only from compliant devices.</span></span> <span data-ttu-id="36810-125">Pour être conforme, votre appareil doit être joint à votre annuaire Active Directory local ou à votre système Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36810-125">To be compliant, your device must be either joined to your on-premises Active Directory or joined to your Azure Active Directory.</span></span>

<span data-ttu-id="36810-126">Vous pouvez facilement savoir si le fait que vous ne puissiez pas accéder à une ressource est lié à l’utilisation d’un appareil non conforme, en consultant la section des détails de la page d’erreur :</span><span class="sxs-lookup"><span data-stu-id="36810-126">You can easily identify whether you can't access a resource due to a device that is not compliant by looking at the details section of the error page:</span></span>
 
<span data-ttu-id="36810-127">![Messages d’accès refusé aux appareils non enregistrés](./media/active-directory-conditional-access-device-remediation/01.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="36810-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="36810-128">Votre appareil est joint à un annuaire Active Directory local ?</span><span class="sxs-lookup"><span data-stu-id="36810-128">Is your device joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="36810-129">**Si la réponse est oui, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36810-129">**If your device is joined to an on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="36810-130">Vérifiez que vous êtes connecté à Windows à l’aide de votre compte professionnel (votre compte Active Directory).</span><span class="sxs-lookup"><span data-stu-id="36810-130">Make sure that you sign in to Windows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="36810-131">Connectez-vous à votre réseau d’entreprise via un réseau privé virtuel (VPN) ou DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="36810-131">Connect to your corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="36810-132">Une fois connecté, appuyez sur la touche Windows + la touche L pour verrouiller votre session Windows.</span><span class="sxs-lookup"><span data-stu-id="36810-132">After you are connected, press the Windows logo key + the L key to lock your Windows session.</span></span>
4. <span data-ttu-id="36810-133">Déverrouillez votre session Windows en saisissant les informations d’identification de votre compte de travail.</span><span class="sxs-lookup"><span data-stu-id="36810-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="36810-134">Attendez une minute, puis essayez d’accéder à nouveau à l’application ou au service.</span><span class="sxs-lookup"><span data-stu-id="36810-134">Wait for a minute, and then try again to access the application or service.</span></span>
6. <span data-ttu-id="36810-135">Si la même page s’affiche, cliquez sur **More details (Plus d'informations)** puis contactez votre administrateur et fournissez les informations demandées.</span><span class="sxs-lookup"><span data-stu-id="36810-135">If you see the same page, click the **More details** link, and then contact your administrator with the details.</span></span>


### <a name="is-your-device-not-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="36810-136">Votre appareil n’est pas joint à un annuaire Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="36810-136">Is your device not joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="36810-137">Dans ce cas, si votre appareil exécute Windows 10, vous avez deux possibilités :</span><span class="sxs-lookup"><span data-stu-id="36810-137">If your device is not joined to an on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="36810-138">Exécuter Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="36810-138">Run Azure AD Join</span></span>
* <span data-ttu-id="36810-139">Ajouter votre compte professionnel ou scolaire à Windows</span><span class="sxs-lookup"><span data-stu-id="36810-139">Add your work or school account to Windows</span></span>

<span data-ttu-id="36810-140">Pour plus d’informations sur les différences entre ces options, consultez la section [Utilisation d’appareils Windows 10 sur votre lieu de travail](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="36810-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="36810-141">Ainsi :</span><span class="sxs-lookup"><span data-stu-id="36810-141">If your device:</span></span>

- <span data-ttu-id="36810-142">Si votre appareil appartient à l’organisation, exécutez l’option Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="36810-142">Belongs to your organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="36810-143">S’il s’agit d’un appareil personnel ou Windows Phone, ajoutez votre compte professionnel ou scolaire à Windows.</span><span class="sxs-lookup"><span data-stu-id="36810-143">Is a personal device or a Windows phone, you should add your work or school account to Windows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="36810-144">Exécution de l’option Azure AD Join sur Windows 10</span><span class="sxs-lookup"><span data-stu-id="36810-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="36810-145">Les étapes permettant de joindre votre appareil à Azure AD sont liées à la version de Windows 10 en cours d’exécution sur ce système.</span><span class="sxs-lookup"><span data-stu-id="36810-145">The steps to join your device to Azure AD are tied the version of Windows 10 you are running on it.</span></span> <span data-ttu-id="36810-146">Pour déterminer la version du système d’exploitation Windows 10, exécutez la commande **winver** :</span><span class="sxs-lookup"><span data-stu-id="36810-146">To determine the version of your Windows 10 operating system, run the **winver** command:</span></span> 

![Version de Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="36810-148">**Mise à jour anniversaire Windows 10 (version 1607) :**</span><span class="sxs-lookup"><span data-stu-id="36810-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="36810-149">Ouvrez l’application **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="36810-149">Open the **Settings** app.</span></span>
2. <span data-ttu-id="36810-150">Cliquez sur **Comptes** > **Access work or school** (Accès professionnel ou scolaire).</span><span class="sxs-lookup"><span data-stu-id="36810-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="36810-151">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="36810-151">Click **Connect**.</span></span>
4. <span data-ttu-id="36810-152">Cliquez sur **Joindre cet appareil à Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="36810-152">Click **Join this device to Azure AD**.</span></span>
5. <span data-ttu-id="36810-153">Authentifiez-vous auprès de votre organisation, fournissez une authentification multifacteur si nécessaire, et suivez la procédure indiquée.</span><span class="sxs-lookup"><span data-stu-id="36810-153">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
6. <span data-ttu-id="36810-154">Déconnectez-vous puis reconnectez-vous à l’aide de votre compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="36810-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="36810-155">Essayez d’accéder à nouveau à l’application.</span><span class="sxs-lookup"><span data-stu-id="36810-155">Try again to access the application.</span></span>

<span data-ttu-id="36810-156">**Mise à jour Windows 10 de novembre 2015 (version 1511) :**</span><span class="sxs-lookup"><span data-stu-id="36810-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="36810-157">Ouvrez l’application **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="36810-157">Open the **Settings** app.</span></span>
2. <span data-ttu-id="36810-158">Cliquez sur **Système** > **À propos de**.</span><span class="sxs-lookup"><span data-stu-id="36810-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="36810-159">Cliquez sur **Joindre Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="36810-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="36810-160">Authentifiez-vous auprès de votre organisation, fournissez une authentification multifacteur si nécessaire, et suivez la procédure indiquée.</span><span class="sxs-lookup"><span data-stu-id="36810-160">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="36810-161">Déconnectez-vous et reconnectez-vous à l’aide de votre compte professionnel (votre compte Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36810-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="36810-162">Essayez d’accéder à nouveau à l’application.</span><span class="sxs-lookup"><span data-stu-id="36810-162">Try again to access the application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="36810-163">Workplace Join pour Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="36810-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="36810-164">Si votre appareil n’est pas joint au domaine et exécute Windows 8.1, vous pouvez procéder à une jonction d’espace de travail et vous inscrire auprès de Microsoft Intune en appliquant la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="36810-164">If your device is not domain-joined and runs Windows 8.1, to do a Workplace Join and enroll in Microsoft Intune, do the following steps:</span></span>

1. <span data-ttu-id="36810-165">Ouvrez **Paramètres du PC**.</span><span class="sxs-lookup"><span data-stu-id="36810-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="36810-166">Cliquez sur **Réseau** > **Espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="36810-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="36810-167">Cliquez sur **Joindre**.</span><span class="sxs-lookup"><span data-stu-id="36810-167">Click **Join**.</span></span>
4. <span data-ttu-id="36810-168">Authentifiez-vous auprès de votre organisation, fournissez une authentification multifacteur si nécessaire, et suivez la procédure indiquée.</span><span class="sxs-lookup"><span data-stu-id="36810-168">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="36810-169">Cliquez sur **Activer**.</span><span class="sxs-lookup"><span data-stu-id="36810-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="36810-170">Essayez d’accéder à nouveau à l’application.</span><span class="sxs-lookup"><span data-stu-id="36810-170">Try again to access the application.</span></span>



#### <a name="add-your-work-or-school-account-to-windows"></a><span data-ttu-id="36810-171">Ajouter votre compte professionnel ou scolaire à Windows</span><span class="sxs-lookup"><span data-stu-id="36810-171">Add your work or school account to Windows</span></span> 


<span data-ttu-id="36810-172">**Mise à jour anniversaire Windows 10 (version 1607) :**</span><span class="sxs-lookup"><span data-stu-id="36810-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="36810-173">Ouvrez l’application **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="36810-173">Open the **Settings** app.</span></span>
2. <span data-ttu-id="36810-174">Cliquez sur **Comptes** > **Access work or school** (Accès professionnel ou scolaire).</span><span class="sxs-lookup"><span data-stu-id="36810-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="36810-175">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="36810-175">Click **Connect**.</span></span>
4. <span data-ttu-id="36810-176">Authentifiez-vous auprès de votre organisation, fournissez une authentification multifacteur si nécessaire, et suivez la procédure indiquée.</span><span class="sxs-lookup"><span data-stu-id="36810-176">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="36810-177">Essayez d’accéder à nouveau à l’application.</span><span class="sxs-lookup"><span data-stu-id="36810-177">Try again to access the application.</span></span>


<span data-ttu-id="36810-178">**Mise à jour Windows 10 de novembre 2015 (version 1511) :**</span><span class="sxs-lookup"><span data-stu-id="36810-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="36810-179">Ouvrez l’application **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="36810-179">Open the **Settings** app.</span></span>
2. <span data-ttu-id="36810-180">Cliquez sur **Comptes** > **Vos comptes**.</span><span class="sxs-lookup"><span data-stu-id="36810-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="36810-181">Cliquez sur **Ajouter un compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="36810-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="36810-182">Authentifiez-vous auprès de votre organisation, fournissez une authentification multifacteur si nécessaire, et suivez la procédure indiquée.</span><span class="sxs-lookup"><span data-stu-id="36810-182">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="36810-183">Essayez d’accéder à nouveau à l’application.</span><span class="sxs-lookup"><span data-stu-id="36810-183">Try again to access the application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="36810-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36810-184">Next steps</span></span>
[<span data-ttu-id="36810-185">Accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36810-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

