---
title: gestion de toodevice aaaIntroduction dans Azure Active Directory | Documents Microsoft
description: "Découvrez comment la gestion des appareils peut vous aider à tooget contrôler les appareils hello qui accèdent à des ressources dans votre environnement."
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
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="c1452-103">Gestion de toodevice introduction dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1452-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="c1452-104">Dans un monde mobile en premier, privilégie le cloud, Azure Active Directory (Azure AD) permet de toodevices de l’authentification unique, les applications et services à partir de n’importe quel endroit.</span><span class="sxs-lookup"><span data-stu-id="c1452-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="c1452-105">Avec la prolifération de hello de périphériques - y compris votre propre appareil BYOD (Bring), les professionnels de l’informatique sont confrontés à deux objectifs différents :</span><span class="sxs-lookup"><span data-stu-id="c1452-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="c1452-106">Permettre aux toobe des utilisateurs finaux hello productif où et quand</span><span class="sxs-lookup"><span data-stu-id="c1452-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="c1452-107">Protéger les ressources d’entreprise de hello à tout moment</span><span class="sxs-lookup"><span data-stu-id="c1452-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="c1452-108">Par le biais des appareils, vos utilisateurs accèdent tooyour des ressources d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c1452-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="c1452-109">tooprotect vos ressources d’entreprise, comme un administrateur, vous voulez contrôler toohave ces appareils.</span><span class="sxs-lookup"><span data-stu-id="c1452-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="c1452-110">Cela vous permet de toomake sûr que vos utilisateurs sont l’accès à vos ressources à partir de périphériques qui répondent à vos normes de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="c1452-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="c1452-111">Gestion des appareils est également foundation hello pour [accès conditionnel basés sur le périphérique](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c1452-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="c1452-112">Avec un accès conditionnel basé sur un appareil, vous pouvez vous assurer qu’accès tooresources dans votre environnement est possible seulement avec les appareils de confiance.</span><span class="sxs-lookup"><span data-stu-id="c1452-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="c1452-113">Cette rubrique explique comment fonctionne la gestion des appareils dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1452-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="c1452-114">Mise en route d’appareils sous contrôle de code hello d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1452-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="c1452-115">tooget un appareil sous contrôle de code hello d’Azure AD, vous avez deux options :</span><span class="sxs-lookup"><span data-stu-id="c1452-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="c1452-116">Inscription</span><span class="sxs-lookup"><span data-stu-id="c1452-116">Registering</span></span> 
- <span data-ttu-id="c1452-117">Jonction</span><span class="sxs-lookup"><span data-stu-id="c1452-117">Joining</span></span>

<span data-ttu-id="c1452-118">**L’enregistrement** un tooAzure appareil AD permet de vous toomanage les identités d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="c1452-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="c1452-119">Lorsqu’un appareil est inscrit, inscription des appareils Azure AD fournit appareil hello avec une identité qui est utilisé tooauthenticate hello périphérique lorsqu’un utilisateur se connecte en tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="c1452-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="c1452-120">Vous pouvez utiliser hello identité tooenable ou désactiver un périphérique.</span><span class="sxs-lookup"><span data-stu-id="c1452-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="c1452-121">Lorsqu’il est associé à une solution de management(MDM) des appareils mobiles tels que Microsoft Intune, les attributs d’appareil hello dans Azure AD sont mises à jour des informations supplémentaires sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="c1452-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="c1452-122">Cela vous permet des règles d’accès conditionnel toocreate qui permettent d’accéder à partir d’appareils toomeet vos normes de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="c1452-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="c1452-123">Pour plus d’informations sur l’inscription d’appareils dans Microsoft Intune, consultez Inscrire des appareils pour la gestion dans Intune.</span><span class="sxs-lookup"><span data-stu-id="c1452-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="c1452-124">**Jointure** un appareil est une extension de tooregistering un appareil.</span><span class="sxs-lookup"><span data-stu-id="c1452-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="c1452-125">Cela signifie que, il vous offre tous les avantages de hello de l’inscription d’un appareil et toothis de plus, il modifie également l’état local de hello d’un périphérique.</span><span class="sxs-lookup"><span data-stu-id="c1452-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="c1452-126">La modification d’état local de hello permet à votre périphérique dans toosign tooa des utilisateurs à l’aide d’une organisation compte professionnel ou scolaire au lieu d’un compte personnel.</span><span class="sxs-lookup"><span data-stu-id="c1452-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="c1452-127">Appareils inscrits sur Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1452-127">Azure AD registered devices</span></span>   

<span data-ttu-id="c1452-128">Bonjour Azure AD inscrit les appareils vise tooprovide vous avec prise en charge pour hello **propre appareil BYOD (Bring Your)** scénario.</span><span class="sxs-lookup"><span data-stu-id="c1452-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="c1452-129">Dans ce scénario, un utilisateur peut accéder aux ressources contrôlées Azure Active Directory de votre organisation à l’aide d’un appareil personnel.</span><span class="sxs-lookup"><span data-stu-id="c1452-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Appareils inscrits sur Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="c1452-131">accès de Hello est basé sur un compte professionnel ou scolaire qui a été saisi sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="c1452-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="c1452-132">Par exemple, Windows 10 permet aux utilisateurs tooadd un travail ou scolaire compte tooa ordinateur personnel, une tablette ou téléphone.</span><span class="sxs-lookup"><span data-stu-id="c1452-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="c1452-133">Lorsqu’un utilisateur a ajouté un travail ou un compte scolaire, un périphérique de hello est inscrit auprès d’Azure AD et éventuellement inscrits dans le système de gestion des appareils mobiles hello que votre organisation a configuré.</span><span class="sxs-lookup"><span data-stu-id="c1452-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="c1452-134">Les utilisateurs de votre organisation peuvent ajouter un travail ou scolaire appareil personnel de compte tooa pour des raisons pratiques :</span><span class="sxs-lookup"><span data-stu-id="c1452-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="c1452-135">Lors de l’accès à une application de travail pour hello pour la première fois</span><span class="sxs-lookup"><span data-stu-id="c1452-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="c1452-136">Manuellement via hello **paramètres** menu dans les cas de hello de Windows 10</span><span class="sxs-lookup"><span data-stu-id="c1452-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="c1452-137">Vous pouvez configurer les appareils inscrits sur Azure AD pour Windows 10, iOS, Android et macOS.</span><span class="sxs-lookup"><span data-stu-id="c1452-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="c1452-138">Appareils joints Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1452-138">Azure AD joined devices</span></span>

<span data-ttu-id="c1452-139">Hello vise des périphériques d’Azure AD joint toosimplify :</span><span class="sxs-lookup"><span data-stu-id="c1452-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="c1452-140">Les déploiements Windows des appareils professionnels</span><span class="sxs-lookup"><span data-stu-id="c1452-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="c1452-141">Accès aux applications tooorganizational et les ressources à partir de n’importe quel appareil Windows</span><span class="sxs-lookup"><span data-stu-id="c1452-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Appareils inscrits sur Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="c1452-143">Ces objectifs sont effectuées en fournissant aux utilisateurs une expérience de libre-service pour l’obtention de travail des appareils sous contrôle de code hello d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1452-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="c1452-144">**Azure AD Join** est destiné aux organisations axées en priorité ou uniquement sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="c1452-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="c1452-145">Ce sont généralement les petites et moyennes entreprises qui ne possèdent pas d’infrastructure Windows Server Active Directory en local.</span><span class="sxs-lookup"><span data-stu-id="c1452-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="c1452-146">Implémentation des appareils Azure AD joint offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c1452-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="c1452-147">**Single-Sign-On (SSO)** tooyour Azure managed services et applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="c1452-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="c1452-148">Vos utilisateurs ne voient pas les invites d’authentification supplémentaires lorsqu’ils accèdent aux ressources de travail.</span><span class="sxs-lookup"><span data-stu-id="c1452-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="c1452-149">Hello fonctionnalité SSO est même lorsqu’ils ne sont pas connectés toohello réseau de domaine disponible.</span><span class="sxs-lookup"><span data-stu-id="c1452-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="c1452-150">**L’itinérance compatible avec l’entreprise** des paramètres utilisateur sur les appareils joints.</span><span class="sxs-lookup"><span data-stu-id="c1452-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="c1452-151">Les utilisateurs ne doivent tooconnect un paramètres toosee de compte (par exemple, Hotmail) Microsoft pour les appareils.</span><span class="sxs-lookup"><span data-stu-id="c1452-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="c1452-152">**Accès tooWindows Store Pro** à l’aide du compte Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1452-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="c1452-153">Les utilisateurs peuvent choisir à partir d’un inventaire des applications présélectionnée par l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="c1452-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="c1452-154">**Windows Hello** prise en charge pour les ressources toowork un accès sécurisé et pratique.</span><span class="sxs-lookup"><span data-stu-id="c1452-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="c1452-155">**Restriction d’accès** tooapps à partir d’uniquement les périphériques qui répondent à la stratégie de conformité.</span><span class="sxs-lookup"><span data-stu-id="c1452-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="c1452-156">Bien qu’Azure AD Join soit principalement conçu pour les organisations qui ne disposent pas d’une infrastructure Windows Server Active Directory locale, vous pouvez également l’utiliser dans les scénarios où :</span><span class="sxs-lookup"><span data-stu-id="c1452-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="c1452-157">Vous ne pouvez pas utiliser une jointure de domaine local, par exemple, si vous avez besoin de tooget des appareils mobiles tels que les tablettes et téléphones sous contrôle de code.</span><span class="sxs-lookup"><span data-stu-id="c1452-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="c1452-158">Vos utilisateurs doivent principalement tooaccess Office 365 ou autres applications SaaS intégrées à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1452-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="c1452-159">Vous voulez toomanage un groupe d’utilisateurs dans Azure AD et non dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1452-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="c1452-160">Par exemple, cela peut concerner tooseasonal employés, prestataires de service ou les étudiants.</span><span class="sxs-lookup"><span data-stu-id="c1452-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="c1452-161">Vous souhaitez tooprovide jointure tooworkers de fonctionnalités dans les succursales distantes avec l’infrastructure locale limitée.</span><span class="sxs-lookup"><span data-stu-id="c1452-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="c1452-162">Vous pouvez configurer des appareils joints Azure AD pour les appareils Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c1452-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="c1452-163">Appareils joints Azure AD hybrides</span><span class="sxs-lookup"><span data-stu-id="c1452-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="c1452-164">Pour plus de dix ans, de nombreuses organisations utilisent hello domaine jointure tootheir locale Active Directory tooenable :</span><span class="sxs-lookup"><span data-stu-id="c1452-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="c1452-165">INFORMATIQUE départements toomanage travail des appareils à partir d’un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="c1452-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="c1452-166">Toosign d’utilisateurs dans les appareils tootheir avec leur annuaire Active Directory de travail ou d’établissement scolaire.</span><span class="sxs-lookup"><span data-stu-id="c1452-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="c1452-167">En règle générale, les organisations avec un encombrement local s’appuient sur les appareils tooprovision méthodes de création d’images, et qu’ils utilisent souvent **System Center Configuration Manager (SCCM)** ou **(GP) de la stratégie de groupe** toomanage les.</span><span class="sxs-lookup"><span data-stu-id="c1452-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="c1452-168">Si votre environnement comporte un site local encombrement d’Active Directory et que vous également tirent parti de fonctionnalités hello fournies par Azure Active Directory, vous pouvez implémenter hybrides Azure AD joint périphériques.</span><span class="sxs-lookup"><span data-stu-id="c1452-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="c1452-169">Il s’agit des appareils qui sont à la fois, jointes tooyour locaux Active Directory et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1452-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Appareils inscrits sur Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="c1452-171">Vous devez utiliser des appareils joints Azure AD hybrides si :</span><span class="sxs-lookup"><span data-stu-id="c1452-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="c1452-172">Vous avez Win32 applications déployées toothese périphériques qui utilisent NTLM / Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c1452-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="c1452-173">Vous avez besoin de stratégie de groupe ou SCCM / appareils de toomanage DCM.</span><span class="sxs-lookup"><span data-stu-id="c1452-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="c1452-174">Vous souhaitez que les appareils de la tooconfigure toocontinue toouse de solutions d’acquisition d’images pour vos employés.</span><span class="sxs-lookup"><span data-stu-id="c1452-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="c1452-175">Vous pouvez configurer des appareils joints Azure AD hybrides pour Windows 10 et des appareils de bas niveau comme Windows 8 et Windows 7.</span><span class="sxs-lookup"><span data-stu-id="c1452-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="c1452-176">Résumé</span><span class="sxs-lookup"><span data-stu-id="c1452-176">Summary</span></span>

<span data-ttu-id="c1452-177">La gestion des périphériques dans Azure AD vous permet de :</span><span class="sxs-lookup"><span data-stu-id="c1452-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="c1452-178">Simplifier les processus hello consistant à placer les appareils sous contrôle de code hello d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1452-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="c1452-179">Fournir à vos utilisateurs avec les ressources de cloud toouse facilement accès tooyour d’une organisation</span><span class="sxs-lookup"><span data-stu-id="c1452-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="c1452-180">En règle générale, vous devez utiliser :</span><span class="sxs-lookup"><span data-stu-id="c1452-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="c1452-181">Les appareils inscrits sur Azure AD pour les appareils personnels</span><span class="sxs-lookup"><span data-stu-id="c1452-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="c1452-182">Appareils joints à Azure AD pour les appareils qui ne sont pas joints à un tooan AD local</span><span class="sxs-lookup"><span data-stu-id="c1452-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="c1452-183">Appareils joints à hybrides Azure AD pour les appareils qui sont joints à un tooan AD local</span><span class="sxs-lookup"><span data-stu-id="c1452-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="c1452-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1452-184">Next steps</span></span>

- <span data-ttu-id="c1452-185">tooget une vue d’ensemble de comment appareil toomanage dans hello Azure portail, consultez [la gestion des appareils à l’aide de hello portail Azure](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c1452-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="c1452-186">toolearn en savoir plus sur l’accès conditionnel basé sur un appareil, consultez [configurer des stratégies d’accès conditionnel basés sur le périphérique Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c1452-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="c1452-187">appareils de Azure AD joint toosetup hybride, consultez [comment tooconfigure hybride Azure Active Directory appareils joints à un](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="c1452-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


