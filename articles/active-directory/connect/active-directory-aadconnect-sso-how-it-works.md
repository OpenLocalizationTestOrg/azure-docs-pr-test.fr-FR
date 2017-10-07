---
title: "Azure AD Connect : authentification unique transparente - Fonctionnement | Microsoft Docs"
description: "Cet article décrit le fonctionne de la fonctionnalité d’Azure Active Directory transparente Single Sign-On hello."
services: active-directory
keywords: "Qu’est-ce qu’Azure AD Connect, Installation d’Active Directory, Composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="0ae2f-104">Authentification unique transparente Azure Active Directory : immersion technique</span><span class="sxs-lookup"><span data-stu-id="0ae2f-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="0ae2f-105">Cet article vous donne des détails techniques dans le fonctionne de la fonctionnalité d’Azure Active Directory transparente Single Sign-On (l’authentification unique transparente) hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0ae2f-106">fonctionnalité d’authentification unique transparente Hello est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="0ae2f-107">Fonctionnement de l’authentification unique transparente (SSO)</span><span class="sxs-lookup"><span data-stu-id="0ae2f-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="0ae2f-108">Cette section comporte deux parties tooit :</span><span class="sxs-lookup"><span data-stu-id="0ae2f-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="0ae2f-109">programme d’installation Bonjour de fonctionnalité de l’authentification unique transparente hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="0ae2f-110">Fonctionnement d’une transaction de connexion mono-utilisateur avec l’authentification unique transparente.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="0ae2f-111">Comment la configuration s’opère-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="0ae2f-111">How does set up work?</span></span>

<span data-ttu-id="0ae2f-112">L’authentification unique transparente s’active via Azure AD Connect comme indiqué [ici](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="0ae2f-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="0ae2f-113">Lors de l’activation de fonctionnalité de hello, hello suit se produire :</span><span class="sxs-lookup"><span data-stu-id="0ae2f-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="0ae2f-114">Un compte d’ordinateur nommé `AZUREADSSOACCT` (c’est-à-dire Azure AD) est créé dans votre instance Active Directory (AD) locale.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="0ae2f-115">clé de déchiffrement Kerberos du compte d’ordinateur Hello est partagée en toute sécurité auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="0ae2f-116">En outre, les deux Kerberos noms principaux de service (SPN) sont créés toorepresent deux URL sont utilisées pendant l’authentification dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="0ae2f-117">compte d’ordinateur Hello et les noms principaux de service Kerberos hello sont créés dans chaque forêt Active Directory vous synchronisez tooAzure AD (à l’aide d’Azure AD Connect) et pour les utilisateurs dont vous souhaitez l’authentification unique transparente.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="0ae2f-118">Déplacer hello `AZUREADSSOACCT` tooan de compte d’ordinateur unité organisation (UO) où les autres comptes d’ordinateur sont stockée tooensure qui il est géré dans hello la même façon et n’est pas supprimé.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0ae2f-119">Il est fortement recommandé que vous [substituer la clé de déchiffrement hello Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) Hello `AZUREADSSOACCT` compte d’ordinateur au moins tous les 30 jours.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="0ae2f-120">Comment s’opère une connexion avec l’authentification unique transparente ?</span><span class="sxs-lookup"><span data-stu-id="0ae2f-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="0ae2f-121">Une fois l’installation de hello est terminée, l’authentification unique transparente fonctionne hello même façon que n’importe quel autre connectez-vous qui utilise l’authentification Windows (intégrée).</span><span class="sxs-lookup"><span data-stu-id="0ae2f-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="0ae2f-122">flux de Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ae2f-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="0ae2f-123">utilisateur de Hello tente tooaccess une application (par exemple, hello Outlook Web App - https://outlook.office365.com/owa/) à partir d’un appareil d’entreprise à un domaine à l’intérieur de votre réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="0ae2f-124">Si l’utilisateur de hello n’est pas déjà inscrit, utilisateur de hello est redirigé toohello Azure AD-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="0ae2f-125">Si la demande de connexion hello Azure AD inclut un `domain_hint` (identifiant votre locataire - par exemple, contoso.onmicrosoft.com) ou `login_hint` (identifiant utilisateur hello - par exemple, user@contoso.onmicrosoft.com ou user@contoso.com) paramètre, puis l’étape 2 est ignorée.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="0ae2f-126">types d’utilisateur Hello dans leur nom d’utilisateur dans la page de connexion hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="0ae2f-127">Azure AD à l’aide de JavaScript dans l’arrière-plan de hello, défis hello navigateur, via une réponse non autorisé 401, tooprovide un ticket Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="0ae2f-128">navigateur de Hello, à son tour, demande un ticket à partir d’Active Directory pour hello `AZUREADSSOACCT` compte d’ordinateur (c'est-à-dire, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ae2f-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="0ae2f-129">Active Directory recherche de compte d’ordinateur hello et retourne un navigateur toohello de ticket Kerberos crypté avec mot de passe du compte d’ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="0ae2f-130">navigateur de Hello transfère le ticket Kerberos de hello elle acquis à partir d’Active Directory tooAzure AD (sur l’un des hello [Azure AD URL ajouté précédemment des paramètres de la zone Intranet du navigateur toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="0ae2f-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="0ae2f-131">Azure AD déchiffre hello ticket Kerberos, qui inclut l’identité hello d’utilisateur hello connecté à un appareil d’entreprise hello, à l’aide de hello précédemment de clé partagée.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="0ae2f-132">Après l’évaluation, Azure AD retourne une application de jeton toohello précédent ou demande hello utilisateur tooperform preuves supplémentaires, telles que l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="0ae2f-133">Si l’authentification utilisateur hello dans réussit, utilisateur de hello est application hello de tooaccess en mesure de.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="0ae2f-134">Hello diagramme suivant illustre tous les composants de hello et étapes hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Authentification unique transparente](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="0ae2f-136">L’authentification unique transparente est opportuniste, ce qui signifie qu’en cas d’échec, expérience de connexion hello revient comportement normal de tooits - c'est-à-dire, hello utilisateur doit tooenter toosign de leur mot de passe dans.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ae2f-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ae2f-137">Next steps</span></span>

- <span data-ttu-id="0ae2f-138">[**Démarrage rapide**](active-directory-aadconnect-sso-quick-start.md) : découvrez l’authentification unique transparente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="0ae2f-139">[**Forum aux Questions** ](active-directory-aadconnect-sso-faq.md) -réponses elles sonttrop aux questions.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="0ae2f-140">[**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-sso.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="0ae2f-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour le dépôt de nouvelles demandes de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="0ae2f-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
