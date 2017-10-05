---
title: "Configuration d’Azure AD Join pour vos utilisateurs | Microsoft Docs"
description: "Explique comment les administrateurs peuvent configurer Azure AD Join pour l’inscription locale d’appareils et d’annuaires."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="775f0-103">Configuration d’Azure AD Join dans votre organisation</span><span class="sxs-lookup"><span data-stu-id="775f0-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="775f0-104">Avant de configurer Azure Active Directory Join (Azure AD Join), vous devez synchroniser votre annuaire local d’utilisateurs avec le cloud ou créer manuellement les comptes gérés dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="775f0-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="775f0-105">Des instructions détaillées pour la synchronisation de vos utilisateurs locaux avec Azure AD sont disponibles dans [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="775f0-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="775f0-106">Pour créer et gérer manuellement des utilisateurs dans Azure AD, reportez-vous à [Gestion des utilisateurs dans Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="775f0-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="775f0-107">Configuration de l’inscription des appareils</span><span class="sxs-lookup"><span data-stu-id="775f0-107">Set up device registration</span></span>
1. <span data-ttu-id="775f0-108">Connectez-vous au portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="775f0-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="775f0-109">Dans le volet gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="775f0-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="775f0-110">Dans l’onglet **Annuaire** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="775f0-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="775f0-111">Sélectionnez l'onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="775f0-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="775f0-112">Accédez à la section **Appareils** .</span><span class="sxs-lookup"><span data-stu-id="775f0-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="775f0-113">Dans l’onglet **Appareils** , définissez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="775f0-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="775f0-114">**NOMBRE MAXIMAL D’APPAREILS PAR UTILISATEUR**: sélectionnez le nombre maximal d’appareils qu’un utilisateur peut avoir dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="775f0-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="775f0-115">Si un utilisateur atteint ce quota, il ne sera pas en mesure d’ajouter des appareils tant qu’un ou plusieurs appareils existants n’auront pas été supprimés.</span><span class="sxs-lookup"><span data-stu-id="775f0-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="775f0-116">**EXIGER MULTI-FACTOR AUTH POUR JOINDRE DES APPAREILS**: indiquez si les utilisateurs doivent fournir un second facteur d’authentification pour joindre leurs appareils à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="775f0-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="775f0-117">Pour plus d’informations sur Azure Multi-Factor Authentication, consultez [Prise en main avec Azure Multi-Factor Authentication dans le cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="775f0-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="775f0-118">**LES UTILISATEURS PEUVENT JOINDRE DES APPAREILS À AZURE AD**: sélectionnez les utilisateurs et groupes autorisés à joindre des appareils à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="775f0-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="775f0-119">**ADMINISTRATEURS SUPPLÉMENTAIRES SUR LES APPAREILS JOINTS À AZURE AD**: avec Azure AD Premium ou Enterprise Mobility Suite (EMS), vous pouvez choisir les utilisateurs qui bénéficient de droits d’administrateur local sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="775f0-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="775f0-120">Les administrateurs globaux et les propriétaires des appareils bénéficient de droits d’administrateur local par défaut.</span><span class="sxs-lookup"><span data-stu-id="775f0-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="775f0-121"><center>![Configuration de l’inscription des appareils](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="775f0-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="775f0-122">Après avoir configuré Azure AD Join pour vos utilisateurs, ces derniers peuvent se connecter à Azure AD via leurs appareils d’entreprise ou personnels.</span><span class="sxs-lookup"><span data-stu-id="775f0-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="775f0-123">Voici trois scénarios expliquant comment vous pouvez autoriser les utilisateurs à configurer Azure AD Join :</span><span class="sxs-lookup"><span data-stu-id="775f0-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="775f0-124">Les utilisateurs joignent un appareil appartenant à l’entreprise directement à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="775f0-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="775f0-125">Les utilisateurs joignent au domaine un appareil appartenant à l’entreprise à l’annuaire Active Directory local et l’étendent à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="775f0-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="775f0-126">Les utilisateurs ajoutent des comptes professionnels ou scolaires à Windows sur un appareil personnel.</span><span class="sxs-lookup"><span data-stu-id="775f0-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="775f0-127">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="775f0-127">Additional information</span></span>
* [<span data-ttu-id="775f0-128">Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels</span><span class="sxs-lookup"><span data-stu-id="775f0-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="775f0-129">Extension des fonctionnalités du cloud aux appareils Windows 10 via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="775f0-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="775f0-130">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="775f0-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="775f0-131">Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="775f0-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="775f0-132">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="775f0-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

