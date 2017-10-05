---
title: "Présentation de la gestion des appareils dans Azure Active Directory | Microsoft Docs"
description: "Découvrez comment la gestion des appareils peut vous aider à contrôler les appareils qui accèdent aux ressources de votre environnement."
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: bebbdddf6b591ea7e36cbac38b568bce614bb335
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-device-management-in-azure-active-directory"></a><span data-ttu-id="ffd0d-103">Présentation de la gestion des appareils dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffd0d-103">Introduction to device management in Azure Active Directory</span></span>

<span data-ttu-id="ffd0d-104">Tout d’abord, dans un appareil où mobilité et cloud occupent le premier plan, Azure Active Directory (Azure AD) autorise une authentification unique sur les appareils, applications et services depuis n’importe où.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="ffd0d-105">Avec la prolifération des appareils, y compris des appareils Bring Your Own Device (BYOD), les professionnels de l’informatique sont confrontés à deux objectifs contradictoires :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-105">With the proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="ffd0d-106">Permettre aux utilisateurs d’être productifs où et quand ils le veulent</span><span class="sxs-lookup"><span data-stu-id="ffd0d-106">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="ffd0d-107">Protéger les ressources de l’entreprise à tout moment</span><span class="sxs-lookup"><span data-stu-id="ffd0d-107">Protect the corporate assets at any time</span></span>

<span data-ttu-id="ffd0d-108">Grâce aux appareils, les utilisateurs peuvent accéder aux ressources d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-108">Through devices, your users are getting access to your corporate assets.</span></span> <span data-ttu-id="ffd0d-109">Pour protéger vos ressources d’entreprise, en tant qu’administrateur informatique, vous souhaitez avoir le contrôle de ces appareils.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-109">To protect your corporate assets, as an IT administrator, you want to have control over these devices.</span></span> <span data-ttu-id="ffd0d-110">Cela vous permet de vous assurer que vos utilisateurs ont accès à vos ressources à partir d’appareils qui répondent à vos normes de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-110">This enables you to make sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="ffd0d-111">La gestion des appareils est également à la base de [l’accès conditionnel en fonction de l’appareil](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ffd0d-111">Device management is also the foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="ffd0d-112">Avec un accès conditionnel en fonction de l’appareil, vous pouvez garantir que l’accès aux ressources de votre environnement est uniquement possible pour les appareils de confiance.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-112">With device-based conditional access, you can ensure that access to resources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="ffd0d-113">Cette rubrique explique comment fonctionne la gestion des appareils dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-the-control-of-azure-ad"></a><span data-ttu-id="ffd0d-114">Donner le contrôle des appareils à Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffd0d-114">Getting devices under the control of Azure AD</span></span>

<span data-ttu-id="ffd0d-115">Pour donner le contrôle d’un appareil à Azure AD, vous avez deux options :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-115">To get a device under the control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="ffd0d-116">Inscription</span><span class="sxs-lookup"><span data-stu-id="ffd0d-116">Registering</span></span> 
- <span data-ttu-id="ffd0d-117">Jonction</span><span class="sxs-lookup"><span data-stu-id="ffd0d-117">Joining</span></span>

<span data-ttu-id="ffd0d-118">**L’inscription** d’un appareil sur Azure AD vous permet de gérer son identité.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-118">**Registering** a device to Azure AD enables you to manage a device’s identity.</span></span> <span data-ttu-id="ffd0d-119">Lors de l’inscription d’un appareil, Azure AD Device Registration fournit une identité à l’appareil qui sera utilisée pour authentifier l’appareil lors de la connexion de l’utilisateur à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-119">When a device is registered, Azure AD device registration provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD.</span></span> <span data-ttu-id="ffd0d-120">Vous pouvez utiliser cette identité pour activer ou désactiver un appareil.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-120">You can use the identity to enable or disable a device.</span></span>

<span data-ttu-id="ffd0d-121">Quand ils sont associés à une solution de gestion des périphériques mobiles (GPM) comme Microsoft Intune, les attributs de l’appareil dans Azure AD sont mis à jour avec des informations supplémentaires sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure AD are updated with additional information about the device.</span></span> <span data-ttu-id="ffd0d-122">Cela vous permet de créer des règles d’accès conditionnel qui imposent que l’accès à partir des appareils réponde à vos critères de sécurité et de conformité.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-122">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="ffd0d-123">Pour plus d’informations sur l’inscription d’appareils dans Microsoft Intune, consultez Inscrire des appareils pour la gestion dans Intune.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="ffd0d-124">**La jonction** d’un appareil est une extension de l’inscription d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-124">**Joining** a device is an extension to registering a device.</span></span> <span data-ttu-id="ffd0d-125">En d’autres termes, cela vous offre tous les avantages de l’inscription d’un appareil et modifie également l’état local de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-125">This means, it provides you with all the benefits of registering a device and in addition to this, it also changes the local state of a device.</span></span> <span data-ttu-id="ffd0d-126">Modifier l’état local permet à vos utilisateurs de se connecter à un appareil à l’aide d’un compte professionnel ou scolaire d’une organisation au lieu d’un compte personnel.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-126">Changing the local state enables your users to sign-in to a device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="ffd0d-127">Appareils inscrits sur Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffd0d-127">Azure AD registered devices</span></span>   

<span data-ttu-id="ffd0d-128">L’objectif des appareils inscrits sur Azure AD est de permettre la prise en charge du scénario **Bring Your Own Device (BYOD)**.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-128">The goal of Azure AD registered devices is to provide you with support for the **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="ffd0d-129">Dans ce scénario, un utilisateur peut accéder aux ressources contrôlées Azure Active Directory de votre organisation à l’aide d’un appareil personnel.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Appareils inscrits sur Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="ffd0d-131">L’accès repose sur un compte professionnel ou scolaire saisi sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-131">The access is based on a work or school account that has been entered on the device.</span></span>  
<span data-ttu-id="ffd0d-132">Par exemple, Windows 10 permet aux utilisateurs d’ajouter un compte professionnel ou scolaire à un ordinateur personnel, une tablette ou un téléphone.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-132">For example, Windows 10 enables users to add a work or school account to a personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="ffd0d-133">Lorsqu’un utilisateur ajoute un compte professionnel ou scolaire, l’appareil est automatiquement inscrit auprès d’Azure AD, voire éventuellement dans le système de gestion de périphériques mobiles (GPM) que votre organisation a configuré.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-133">When a user has added a work or school account, the device is registered with Azure AD and optionally enrolled in the mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="ffd0d-134">Les utilisateurs de votre organisation peuvent facilement ajouter un compte professionnel ou scolaire à un appareil personnel :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-134">Your organization’s users can add a work or school account to a personal device conveniently:</span></span>

- <span data-ttu-id="ffd0d-135">Pour votre premier accès à une application professionnelle</span><span class="sxs-lookup"><span data-stu-id="ffd0d-135">When accessing a work application for the first time</span></span>
- <span data-ttu-id="ffd0d-136">Manuellement via le menu **Paramètres** dans le cas de Windows 10</span><span class="sxs-lookup"><span data-stu-id="ffd0d-136">Manually via the **Settings** menu in the case of Windows 10</span></span> 

<span data-ttu-id="ffd0d-137">Vous pouvez configurer les appareils inscrits sur Azure AD pour Windows 10, iOS, Android et macOS.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="ffd0d-138">Appareils joints Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffd0d-138">Azure AD joined devices</span></span>

<span data-ttu-id="ffd0d-139">Les appareils joints Azure AD ont pour objectif de simplifier :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-139">The goal of Azure AD joined devices is to simplify:</span></span>

- <span data-ttu-id="ffd0d-140">Les déploiements Windows des appareils professionnels</span><span class="sxs-lookup"><span data-stu-id="ffd0d-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="ffd0d-141">L’accès aux applications et aux ressources d’organisation à partir de n’importe quel appareil Windows</span><span class="sxs-lookup"><span data-stu-id="ffd0d-141">Access to organizational apps and resources from any Windows device</span></span>

![Appareils inscrits sur Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="ffd0d-143">Ces objectifs sont atteints en fournissant aux utilisateurs une expérience libre-service du contrôle des appareils professionnels par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under the control of Azure AD.</span></span>  
<span data-ttu-id="ffd0d-144">**Azure AD Join** est destiné aux organisations axées en priorité ou uniquement sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="ffd0d-145">Ce sont généralement les petites et moyennes entreprises qui ne possèdent pas d’infrastructure Windows Server Active Directory en local.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="ffd0d-146">L’implémentation d’appareils joints Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-146">Implementing Azure AD joined devices provides you with the following benefits:</span></span>

- <span data-ttu-id="ffd0d-147">**L’authentification unique** à vos applications et services SaaS gérés par Azure.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-147">**Single-Sign-On (SSO)** to your Azure managed SaaS apps and services.</span></span> <span data-ttu-id="ffd0d-148">Vos utilisateurs ne voient pas les invites d’authentification supplémentaires lorsqu’ils accèdent aux ressources de travail.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="ffd0d-149">La fonctionnalité d’authentification unique est disponible même lorsqu’ils ne sont pas connectés au réseau de domaine disponible.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-149">The SSO functionality is even when they are not connected to the domain network available.</span></span>

- <span data-ttu-id="ffd0d-150">**L’itinérance compatible avec l’entreprise** des paramètres utilisateur sur les appareils joints.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="ffd0d-151">Les utilisateurs n’ont pas besoin de se connecter à un compte Microsoft (par exemple, Hotmail) pour afficher les paramètres sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-151">Users don’t need to connect a Microsoft account (for example, Hotmail) to see settings across devices.</span></span>

- <span data-ttu-id="ffd0d-152">**Accéder au Windows Store pour Entreprises** à l’aide d’un compte AD.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-152">**Access to Windows Store for Business** using AD account.</span></span> <span data-ttu-id="ffd0d-153">Les utilisateurs peuvent choisir parmi un inventaire d’applications présélectionnées par l’organisation.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-153">Your users can choose from an inventory of applications pre-selected by the organization.</span></span>

- <span data-ttu-id="ffd0d-154">L’assistant **Windows Hello** fournit un accès sécurisé et pratique aux ressources de travail.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-154">**Windows Hello** support for secure and convenient access to work resources.</span></span>

- <span data-ttu-id="ffd0d-155">**La restriction d’accès** aux applications ne s’applique qu’aux appareils qui répondent à la stratégie de conformité.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-155">**Restriction of access** to apps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="ffd0d-156">Bien qu’Azure AD Join soit principalement conçu pour les organisations qui ne disposent pas d’une infrastructure Windows Server Active Directory locale, vous pouvez également l’utiliser dans les scénarios où :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="ffd0d-157">Vous ne pouvez pas utiliser de jonction de domaine locale, par exemple, si vous avez besoin de contrôler des appareils mobiles, tels que des tablettes et des téléphones.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-157">You can’t use an on-premises domain join, for example, if you need to get mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="ffd0d-158">Vos utilisateurs ont principalement besoin d’accéder à Office 365 ou d’autres applications SaaS intégrées à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-158">Your users primarily need to access Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="ffd0d-159">Vous souhaitez gérer un groupe d’utilisateurs dans Azure AD et non dans un répertoire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-159">You want to manage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="ffd0d-160">Par exemple, cela peut concerner les travailleurs saisonniers, les prestataires ou les étudiants.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-160">This can apply, for example, to seasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="ffd0d-161">Vous souhaitez fournir des fonctionnalités de jonction aux travailleurs dans des succursales distantes avec une infrastructure locale limitée.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-161">You want to provide joining capabilities to workers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="ffd0d-162">Vous pouvez configurer des appareils joints Azure AD pour les appareils Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="ffd0d-163">Appareils joints Azure AD hybrides</span><span class="sxs-lookup"><span data-stu-id="ffd0d-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="ffd0d-164">Pendant plus de dix ans, de nombreuses organisations ont utilisé la jonction de domaine dans leur répertoire Active Directory local pour permettre :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-164">For more than a decade, many organizations have used the domain join to their on-premises Active Directory to enable:</span></span>

- <span data-ttu-id="ffd0d-165">Aux services informatiques de gérer les appareils professionnels à partir d’un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-165">IT departments to manage work-owned devices from a central location.</span></span>

- <span data-ttu-id="ffd0d-166">Aux utilisateurs de se connecter à leurs appareils à partir de leurs comptes Active Directory professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-166">Users to sign in to their devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="ffd0d-167">En règle générale, les organisations disposant d’empreintes locales s’appuient sur des méthodes de création d’images pour approvisionner les appareils. Ils utilisent souvent **System Center Configuration Manager (SCCM)** ou les **stratégies de groupe** pour les gérer.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-167">Typically, organizations with an on-premises footprint rely on imaging methods to provision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** to manage them.</span></span>

<span data-ttu-id="ffd0d-168">Si votre environnement comporte une empreinte locale AD et vous souhaitez également profiter des fonctionnalités proposées par Azure Active Directory, vous pouvez implémenter les appareils joints Azure AD hybrides.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-168">If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="ffd0d-169">Il s’agit d’appareils qui sont à la fois, joints à votre service Active Directory local et à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-169">These are devices that are both, joined to your on-premises Active Directory and your Azure Active Directory.</span></span>

![Appareils inscrits sur Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="ffd0d-171">Vous devez utiliser des appareils joints Azure AD hybrides si :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="ffd0d-172">Vous disposez d’applications Win32 déployées sur ces appareils qui utilisent NTLM/Kerberos.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-172">You have Win32 apps deployed to these devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="ffd0d-173">Vous avez besoin de stratégies de groupe ou de SCCM/DCM pour gérer les appareils.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-173">You require GP or SCCM / DCM to manage devices.</span></span>

- <span data-ttu-id="ffd0d-174">Vous souhaitez continuer à utiliser des solutions de création d’images pour configurer les appareils de vos employés.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-174">You want to continue to use imaging solutions to configure devices for your employees.</span></span>

<span data-ttu-id="ffd0d-175">Vous pouvez configurer des appareils joints Azure AD hybrides pour Windows 10 et des appareils de bas niveau comme Windows 8 et Windows 7.</span><span class="sxs-lookup"><span data-stu-id="ffd0d-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="ffd0d-176">Résumé</span><span class="sxs-lookup"><span data-stu-id="ffd0d-176">Summary</span></span>

<span data-ttu-id="ffd0d-177">La gestion des périphériques dans Azure AD vous permet de :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="ffd0d-178">Simplifier le processus consistant à donner le contrôle d’appareils à Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffd0d-178">Simplify the process of bringing devices under the control of Azure AD</span></span>

- <span data-ttu-id="ffd0d-179">Fournir à vos utilisateurs un accès facile aux ressources basées sur le cloud de votre organisation</span><span class="sxs-lookup"><span data-stu-id="ffd0d-179">Provide your users with an easy to use access to your organization’s cloud-based resources</span></span>

<span data-ttu-id="ffd0d-180">En règle générale, vous devez utiliser :</span><span class="sxs-lookup"><span data-stu-id="ffd0d-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="ffd0d-181">Les appareils inscrits sur Azure AD pour les appareils personnels</span><span class="sxs-lookup"><span data-stu-id="ffd0d-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="ffd0d-182">Les appareils joints Azure AD pour les appareils qui ne sont pas joints à un AD local</span><span class="sxs-lookup"><span data-stu-id="ffd0d-182">Azure AD joined devices for devices that are not joined to an on-premises AD</span></span> 

- <span data-ttu-id="ffd0d-183">Les appareils joints Azure AD hybrides pour les appareils joints à un AD local</span><span class="sxs-lookup"><span data-stu-id="ffd0d-183">Hybrid Azure AD joined devices for devices that are joined to an on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="ffd0d-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ffd0d-184">Next steps</span></span>

- <span data-ttu-id="ffd0d-185">Pour obtenir une vue d’ensemble de la gestion des appareils dans le portail Azure, consultez [Gestion des appareils via le portail Azure](device-management-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ffd0d-185">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="ffd0d-186">Pour en savoir plus sur l’accès conditionnel basé sur les appareils, consultez [Configurer les stratégies d’accès conditionnel basé sur les appareils Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ffd0d-186">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="ffd0d-187">Pour configurer les appareils joints Azure AD hybrides, consultez [Comment configurer des appareils joints Azure AD hybrides](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="ffd0d-187">To setup hybrid Azure AD joined devices, see [how to configure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


