---
title: "aaaHow tooconfigure l’inscription automatique des périphériques joints au domaine de Windows avec Azure Active Directory | Documents Microsoft"
description: "Configurer votre tooregister d’appareils Windows joints automatiquement et silencieusement avec Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="82b7e-103">Prise en main du service Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="82b7e-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="82b7e-104">L’inscription de périphérique Azure Active Directory est foundation hello pour les scénarios d’accès conditionnel basés sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="82b7e-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="82b7e-105">Lorsqu’un appareil est inscrit, l’inscription de périphérique Azure Active Directory fournit appareil hello avec une identité qui est utilisé tooauthenticate hello périphérique lorsque hello utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="82b7e-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="82b7e-106">Hello authentifié dispositif et attributs hello du périphérique de hello, peuvent ensuite être des stratégies d’accès conditionnel tooenforce utilisé pour les applications qui sont hébergées dans le cloud de hello et sur site.</span><span class="sxs-lookup"><span data-stu-id="82b7e-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="82b7e-107">Lorsqu’il est associé à une solution de management(MDM) des appareils mobiles tels que Microsoft Intune, les attributs d’appareil hello dans Azure Active Directory sont mis à jour avec des informations supplémentaires sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="82b7e-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="82b7e-108">Cela vous permet des règles d’accès conditionnel toocreate qui permettent d’accéder à partir d’appareils toomeet vos normes de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="82b7e-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="82b7e-109">Pour plus d’informations sur l’inscription d’appareils dans Microsoft Intune, consultez Inscrire des appareils pour la gestion dans Intune.</span><span class="sxs-lookup"><span data-stu-id="82b7e-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="82b7e-110">Les scénarios mis en œuvre par Azure Active Directory Device Registration incluent la prise en charge des appareils iOS, Android et Windows.</span><span class="sxs-lookup"><span data-stu-id="82b7e-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="82b7e-111">Hello les scénarios individuels qui utilisent l’inscription d’Azure Active Directory pour appareils peuvent avoir une plateforme prise en charge et des exigences plus spécifiques.</span><span class="sxs-lookup"><span data-stu-id="82b7e-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="82b7e-112">Ces scénarios sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="82b7e-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="82b7e-113">**Accès conditionnel pour les applications Office 365 avec Microsoft Intune :** administrateurs informatiques peuvent configurer l’accès conditionnel appareil stratégies toosecure ressources d’entreprise, tandis qu’à hello même moment, ce qui permet de travailleurs sur les appareils compatibles services de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="82b7e-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="82b7e-114">Pour plus d’informations, consultez la rubrique Stratégies d’accès conditionnel basées sur les appareils pour les services Office 365.</span><span class="sxs-lookup"><span data-stu-id="82b7e-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="82b7e-115">**Tooapplications d’accès conditionnel qui sont hébergées en local :** vous pouvez utiliser les appareils inscrits avec des stratégies d’accès pour les applications qui sont configurées toouse AD FS avec Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="82b7e-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="82b7e-116">Pour plus d’informations sur la configuration d’un accès conditionnel en local, consultez la rubrique [Configuration d'un accès conditionnel en local à l'aide du service d'inscription d'appareils Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="82b7e-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="82b7e-117">Configuration du service Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="82b7e-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="82b7e-118">l’inscription de périphérique toosetup, vous disposez de plusieurs options :</span><span class="sxs-lookup"><span data-stu-id="82b7e-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="82b7e-119">Les appareils peuvent s’inscrire lorsque tooAzure jointes AD domaine.</span><span class="sxs-lookup"><span data-stu-id="82b7e-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="82b7e-120">Pour plus d’informations sur cette rubrique, vous pouvez plus d’informations sur les paramètres de Azure AD Join et hello requis pour les utilisateurs domaine toojoin Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82b7e-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="82b7e-121">Les appareils peuvent être inscrits lorsque le travail ajouter des utilisateurs ou les comptes de l’école tooWindows sur un appareil personnel ou lorsque les appareils mobiles connectent tooa les ressources de travail nécessitant l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="82b7e-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="82b7e-122">tooensure, vous devez activer l’inscription Azure Active Directory pour appareils dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="82b7e-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="82b7e-123">Les appareils peuvent être inscrits à l’aide d’une inscription automatique pour les ordinateurs traditionnels joints au domaine.</span><span class="sxs-lookup"><span data-stu-id="82b7e-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="82b7e-124">tooensure, vous devez la première installation Azure AD Connect avant de continuer l’inscription automatique.</span><span class="sxs-lookup"><span data-stu-id="82b7e-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="82b7e-125">Pour obtenir des instructions plus récente, consultez [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="82b7e-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="82b7e-126">Vous pouvez également examiner et activer ou désactiver les appareils inscrits via le portail d’administration de hello dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="82b7e-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="82b7e-127">Activer le service d’inscription de hello Azure Active Directory appareils</span><span class="sxs-lookup"><span data-stu-id="82b7e-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="82b7e-128">**hello tooenable service d’inscription de périphérique Azure Active Directory :**</span><span class="sxs-lookup"><span data-stu-id="82b7e-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="82b7e-129">Se connecter toohello portail Microsoft Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="82b7e-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="82b7e-130">Dans le volet gauche de hello, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82b7e-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="82b7e-131">Sur l’onglet du répertoire hello, sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="82b7e-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="82b7e-132">Cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="82b7e-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="82b7e-133">Faites défiler trop**périphériques**.</span><span class="sxs-lookup"><span data-stu-id="82b7e-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="82b7e-134">Sélectionnez TOUS pour LES UTILISATEURS PEUVENT INSCRIRE LEURS APPAREILS SUR AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="82b7e-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="82b7e-135">Sélectionnez le nombre maximal de hello de périphériques souhaités tooauthorize par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82b7e-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="82b7e-136">Hello l’inscription avec Microsoft Intune ou gestion des appareils mobiles pour Office 365 nécessite l’inscription de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="82b7e-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="82b7e-137">Si vous avez configuré l’un de ces services, **TOUS** est sélectionné et **AUCUN** est désactivé.</span><span class="sxs-lookup"><span data-stu-id="82b7e-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="82b7e-138">Veuillez vous assurer qu’ils sont configurés correctement et la gestion des licences appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="82b7e-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="82b7e-139">Par défaut, l’authentification à deux facteurs n’est pas activée pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="82b7e-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="82b7e-140">Elle est toutefois recommandée lors de l’inscription d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="82b7e-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="82b7e-141">Avant de demander une authentification à deux facteurs pour ce service, vous devez configurer un fournisseur d’authentification à deux facteurs dans Azure Active Directory et configurer vos comptes d’utilisateur pour l’authentification multifacteur, consultez Ajout de l’authentification multifacteur tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82b7e-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="82b7e-142">Si vous utilisez les services AD FS avec Windows Server 2012 R2, vous devez configurer un module d’authentification à deux facteurs dans ces services. Pour plus d’informations, consultez la page Utilisation de Multi-Factor Authentication avec les services AD FS (Active Directory Federation Services).</span><span class="sxs-lookup"><span data-stu-id="82b7e-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="82b7e-143">Afficher et gérer des objets appareil dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82b7e-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="82b7e-144">À partir du portail d’administration Azure hello, vous pouvez afficher, bloquer et débloquer des appareils.</span><span class="sxs-lookup"><span data-stu-id="82b7e-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="82b7e-145">Un appareil bloqué n’aura plus accès tooapplications qui sont tooallow configuré uniquement pour les appareils inscrits.</span><span class="sxs-lookup"><span data-stu-id="82b7e-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="82b7e-146">**tooview et gérer des objets appareil dans Azure Active Directory :**</span><span class="sxs-lookup"><span data-stu-id="82b7e-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="82b7e-147">Ouvrez une session toohello portail Microsoft Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="82b7e-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="82b7e-148">Dans le volet gauche de hello, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82b7e-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="82b7e-149">Sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="82b7e-149">Select your directory.</span></span>

4.  <span data-ttu-id="82b7e-150">Sélectionnez **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="82b7e-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="82b7e-151">Cliquez sur utilisateur hello pour lequel vous souhaitez que les appareils de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="82b7e-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="82b7e-152">Sélectionnez **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="82b7e-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="82b7e-153">Sélectionnez **Appareils inscrits**.</span><span class="sxs-lookup"><span data-stu-id="82b7e-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="82b7e-154">Vous pouvez à présent, passez en revue, bloquer ou débloquer des appareils inscrits de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="82b7e-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="82b7e-155">Les appareils Windows 10 qui sont automatiquement inscrits et joint au domaine local n’apparaissent pas sous l’onglet utilisateurs de hello. Utilisez toofind de commande PowerShell de Get-MsolDevice hello tous les périphériques de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="82b7e-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="82b7e-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82b7e-156">Next steps</span></span>

<span data-ttu-id="82b7e-157">toosetup automatisée de l’inscription de périphérique, consultez [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="82b7e-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


