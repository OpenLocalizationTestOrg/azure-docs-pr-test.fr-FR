---
title: "aaaSetting d’Azure AD Join pour vos utilisateurs | Documents Microsoft"
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
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="dd39f-103">Configuration d’Azure AD Join dans votre organisation</span><span class="sxs-lookup"><span data-stu-id="dd39f-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="dd39f-104">Avant de configurer Azure Active Directory Join (Azure AD Join), vous devez tooeither synchronisation vers le haut de votre annuaire local du cloud de toohello les utilisateurs ou créer manuellement des comptes gérés dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd39f-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="dd39f-105">Obtenir des instructions détaillées pour la synchronisation de votre tooAzure d’utilisateurs local AD est couvert dans [intégrer vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="dd39f-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="dd39f-106">toomanually créer et gérer des utilisateurs dans Azure AD, consultez trop[gestion des utilisateurs dans Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd39f-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="dd39f-107">Configuration de l’inscription des appareils</span><span class="sxs-lookup"><span data-stu-id="dd39f-107">Set up device registration</span></span>
1. <span data-ttu-id="dd39f-108">Ouvrez une session toohello portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd39f-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="dd39f-109">Dans le volet gauche de hello, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd39f-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="dd39f-110">Sur hello **répertoire** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="dd39f-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="dd39f-111">Sélectionnez hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="dd39f-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="dd39f-112">Accédez toohello **périphériques** section.</span><span class="sxs-lookup"><span data-stu-id="dd39f-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="dd39f-113">Sur hello **périphériques** définir hello, onglet :</span><span class="sxs-lookup"><span data-stu-id="dd39f-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="dd39f-114">**NOMBRE de périphériques par utilisateur maximale**: sélectionnez hello le nombre maximal d’appareils qu’un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd39f-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="dd39f-115">Si un utilisateur atteint ce quota, elles seront pas en mesure de tooadd des périphériques supplémentaires jusqu'à ce qu’un ou plusieurs des appareils existants sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="dd39f-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="dd39f-116">**EXIGER l’authentification MULTIFACTEUR tooJOIN périphériques**: définir si les utilisateurs sont requis tooprovide une authentification de second facteur toojoin leur tooAzure appareil AD.</span><span class="sxs-lookup"><span data-stu-id="dd39f-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="dd39f-117">Pour plus d’informations sur l’authentification multifacteur Azure, consultez [prise en main d’Azure multi-Factor Authentication dans le cloud de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="dd39f-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="dd39f-118">**Les utilisateurs peuvent les appareils AZURE AD JOIN**: sélectionnez hello utilisateurs et groupes sont autorisés à toojoin périphériques tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="dd39f-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="dd39f-119">**AZURE de ON administrateurs supplémentaires à des appareils joints AD**: avec Azure AD Premium ou hello Enterprise Mobility Suite (EMS), vous pouvez choisir quels utilisateurs sont accordés des droits d’administrateur local toohello appareil.</span><span class="sxs-lookup"><span data-stu-id="dd39f-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="dd39f-120">Les administrateurs globaux et les propriétaires des appareils bénéficient de droits d’administrateur local par défaut.</span><span class="sxs-lookup"><span data-stu-id="dd39f-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="dd39f-121"><center>![Configuration de l’inscription des appareils](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png)</center></span><span class="sxs-lookup"><span data-stu-id="dd39f-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="dd39f-122">Une fois que vous configurez Azure AD Join pour vos utilisateurs, ils peuvent se connecter tooAzure AD via leurs d’entreprise ou appareils personnels.</span><span class="sxs-lookup"><span data-stu-id="dd39f-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="dd39f-123">Voici hello trois scénarios vous pouvez utiliser tooenable tooset de vos utilisateurs d’Azure AD Join :</span><span class="sxs-lookup"><span data-stu-id="dd39f-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="dd39f-124">Les utilisateurs joindre un appareil d’entreprise directement tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="dd39f-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="dd39f-125">Toohello de périphérique aux utilisateurs appartenant à une société de jonction de domaine Active Directory local et puis étend hello appareil tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="dd39f-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="dd39f-126">Ajoutez les utilisateurs du travail ou scolaire comptes tooWindows sur un appareil personnel</span><span class="sxs-lookup"><span data-stu-id="dd39f-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="dd39f-127">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd39f-127">Additional information</span></span>
* [<span data-ttu-id="dd39f-128">Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail</span><span class="sxs-lookup"><span data-stu-id="dd39f-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="dd39f-129">Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="dd39f-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="dd39f-130">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="dd39f-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="dd39f-131">Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="dd39f-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="dd39f-132">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="dd39f-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

