---
title: "Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine | Microsoft Docs"
description: "Configurez vos appareils Windows joints à un domaine pour les inscrire automatiquement et en mode silencieux auprès d’Azure Active Directory."
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="6b505-103">Prise en main du service Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="6b505-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="6b505-104">Azure Active Directory Device Registration est la base des scénarios d’accès conditionnel en fonction de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6b505-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="6b505-105">Lors de l’inscription d’un appareil, Azure Active Directory Device Registration fournit une identité à l’appareil qui sera utilisée pour authentifier cet appareil lors de la connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6b505-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="6b505-106">L’appareil authentifié et les attributs de l’appareil peuvent alors être utilisés pour appliquer des stratégies d’accès conditionnel pour les applications qui sont hébergées sur le cloud et localement.</span><span class="sxs-lookup"><span data-stu-id="6b505-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="6b505-107">Quand ils sont associés à une solution de gestion des appareils mobiles comme Microsoft Intune, les attributs de l’appareil dans Azure Active Directory sont mis à jour avec des informations supplémentaires sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6b505-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="6b505-108">Cela vous permet de créer des règles d’accès conditionnel qui imposent que l’accès à partir des appareils réponde à vos normes de sécurité et de conformité.</span><span class="sxs-lookup"><span data-stu-id="6b505-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="6b505-109">Pour plus d’informations sur l’inscription d’appareils dans Microsoft Intune, consultez Inscrire des appareils pour la gestion dans Intune.</span><span class="sxs-lookup"><span data-stu-id="6b505-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="6b505-110">Les scénarios mis en œuvre par Azure Active Directory Device Registration incluent la prise en charge des appareils iOS, Android et Windows.</span><span class="sxs-lookup"><span data-stu-id="6b505-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="6b505-111">Les scénarios individuels qui utilisent Azure AD Device Registration peuvent avoir une prise en charge des plateformes et des exigences plus spécifiques.</span><span class="sxs-lookup"><span data-stu-id="6b505-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="6b505-112">Ces scénarios sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="6b505-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="6b505-113">**Accès conditionnel pour les applications Office 365 avec Microsoft Intune** : les administrateurs informatiques peuvent configurer des stratégies d’appareil d’accès conditionnel pour sécuriser les ressources d’entreprise, tout en autorisant les professionnels de l’information à accéder aux services sur les appareils conformes.</span><span class="sxs-lookup"><span data-stu-id="6b505-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="6b505-114">Pour plus d’informations, consultez la rubrique Stratégies d’accès conditionnel basées sur les appareils pour les services Office 365.</span><span class="sxs-lookup"><span data-stu-id="6b505-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="6b505-115">**Accès conditionnel aux applications hébergées en local** : vous pouvez utiliser des appareils inscrits avec des stratégies d’accès pour les applications qui sont configurées pour utiliser les services AD FS avec Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6b505-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="6b505-116">Pour plus d’informations sur la configuration d’un accès conditionnel en local, consultez la rubrique [Configuration d'un accès conditionnel en local à l'aide du service d'inscription d'appareils Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="6b505-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="6b505-117">Configuration du service Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="6b505-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="6b505-118">Vous avez plusieurs options pour configurer l’inscription d’appareils :</span><span class="sxs-lookup"><span data-stu-id="6b505-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="6b505-119">Les appareils peuvent être inscrits lorsqu'ils sont joints au domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b505-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="6b505-120">Pour en savoir plus sur ce thème, vous pouvez trouver plus d’informations sur Azure AD Join et sur les paramètres requis pour les utilisateurs afin de joindre le domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b505-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="6b505-121">Les périphériques peuvent être enregistrés lorsque des utilisateurs ajoutent des comptes professionnels ou scolaires à Windows sur un appareil personnel ou lorsque des appareils mobiles se connectent à une ressource professionnelle nécessitant une inscription.</span><span class="sxs-lookup"><span data-stu-id="6b505-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="6b505-122">Pour ce faire, vous devez activer l’inscription Azure AD Device Registration dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b505-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="6b505-123">Les appareils peuvent être inscrits à l’aide d’une inscription automatique pour les ordinateurs traditionnels joints au domaine.</span><span class="sxs-lookup"><span data-stu-id="6b505-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="6b505-124">Pour ce faire, vous devez d'abord configurer Azure AD Connect avant de poursuivre avec l’inscription automatique de l'appareil.</span><span class="sxs-lookup"><span data-stu-id="6b505-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="6b505-125">Pour connaître les instructions actuelles, consultez [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="6b505-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="6b505-126">Vous pouvez également afficher et activer ou désactiver les appareils inscrits par le biais du portail d’administration dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b505-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="6b505-127">Activer le service Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="6b505-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="6b505-128">**Pour activer le service Azure Active Directory Device Registration :**</span><span class="sxs-lookup"><span data-stu-id="6b505-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="6b505-129">Connectez-vous au portail Microsoft Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b505-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="6b505-130">Dans le volet gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b505-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="6b505-131">Sous l’onglet Annuaire, sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="6b505-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="6b505-132">Cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="6b505-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="6b505-133">Accédez à **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="6b505-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="6b505-134">Sélectionnez TOUS pour LES UTILISATEURS PEUVENT INSCRIRE LEURS APPAREILS SUR AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="6b505-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="6b505-135">Sélectionnez le nombre maximal d’appareils que vous souhaitez autoriser par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6b505-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="6b505-136">L’inscription auprès de Microsoft Intune ou de Mobile Device Management pour Office 365 nécessite l’enregistrement de l'appareil.</span><span class="sxs-lookup"><span data-stu-id="6b505-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="6b505-137">Si vous avez configuré l’un de ces services, **TOUS** est sélectionné et **AUCUN** est désactivé.</span><span class="sxs-lookup"><span data-stu-id="6b505-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="6b505-138">Assurez-vous qu’ils sont configurés correctement et disposent des licences appropriées.</span><span class="sxs-lookup"><span data-stu-id="6b505-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="6b505-139">Par défaut, l’authentification à deux facteurs n’est pas activée pour le service.</span><span class="sxs-lookup"><span data-stu-id="6b505-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="6b505-140">Elle est toutefois recommandée lors de l’inscription d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="6b505-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="6b505-141">Avant de demander une authentification à deux facteurs pour ce service, vous devez configurer un fournisseur d’authentification à deux facteurs dans Azure Active Directory et configurer vos comptes d’utilisateur pour Multi-Factor Authentication. Consultez la page Ajout de Multi-Factor Authentication à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b505-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="6b505-142">Si vous utilisez les services AD FS avec Windows Server 2012 R2, vous devez configurer un module d’authentification à deux facteurs dans ces services. Pour plus d’informations, consultez la page Utilisation de Multi-Factor Authentication avec les services AD FS (Active Directory Federation Services).</span><span class="sxs-lookup"><span data-stu-id="6b505-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="6b505-143">Afficher et gérer des objets appareil dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b505-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="6b505-144">Dans le portail d’administration Azure, vous pouvez afficher, bloquer et débloquer des appareils.</span><span class="sxs-lookup"><span data-stu-id="6b505-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="6b505-145">Un appareil bloqué n’aura plus accès aux applications qui sont configurées de manière à n’autoriser que les appareils inscrits.</span><span class="sxs-lookup"><span data-stu-id="6b505-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="6b505-146">**Pour afficher et gérer des objets appareil dans Azure Active Directory :**</span><span class="sxs-lookup"><span data-stu-id="6b505-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="6b505-147">Connectez-vous au portail Microsoft Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b505-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="6b505-148">Dans le volet gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b505-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="6b505-149">Sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="6b505-149">Select your directory.</span></span>

4.  <span data-ttu-id="6b505-150">Sélectionnez **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6b505-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="6b505-151">Cliquez sur l’utilisateur qui doit être autorisé à afficher les appareils.</span><span class="sxs-lookup"><span data-stu-id="6b505-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="6b505-152">Sélectionnez **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="6b505-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="6b505-153">Sélectionnez **Appareils inscrits**.</span><span class="sxs-lookup"><span data-stu-id="6b505-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="6b505-154">Maintenant, vous pouvez réviser, bloquer ou débloquer les appareils inscrits des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6b505-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="6b505-155">Les appareils Windows 10 qui sont joints localement au domaine et enregistrés automatiquement n’apparaissent pas sous l’onglet Utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6b505-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="6b505-156">Utilisez la commande Get-MsolDevice PowerShell pour rechercher tous les appareils de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="6b505-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="6b505-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b505-157">Next steps</span></span>

<span data-ttu-id="6b505-158">Pour configurer l'enregistrement automatique des appareils, consultez la rubrique [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="6b505-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


