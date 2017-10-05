---
title: "Azure AD Connect : authentification unique transparente - Fonctionnement | Microsoft Docs"
description: "Cet article décrit le fonctionnement de la fonctionnalité d’authentification unique transparente d’Azure Active Directory."
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
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="ecf5d-104">Authentification unique transparente Azure Active Directory : immersion technique</span><span class="sxs-lookup"><span data-stu-id="ecf5d-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="ecf5d-105">Cet article vous fournit des détails techniques sur le fonctionnement de la fonctionnalité d’authentification unique (SSO) transparente d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ecf5d-106">La fonctionnalité Authentification unique transparente est en préversion.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="ecf5d-107">Fonctionnement de l’authentification unique transparente (SSO)</span><span class="sxs-lookup"><span data-stu-id="ecf5d-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="ecf5d-108">Cette section se compose de deux parties :</span><span class="sxs-lookup"><span data-stu-id="ecf5d-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="ecf5d-109">Configuration de la fonctionnalité d’authentification unique transparente.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="ecf5d-110">Fonctionnement d’une transaction de connexion mono-utilisateur avec l’authentification unique transparente.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="ecf5d-111">Comment la configuration s’opère-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="ecf5d-111">How does set up work?</span></span>

<span data-ttu-id="ecf5d-112">L’authentification unique transparente s’active via Azure AD Connect comme indiqué [ici](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="ecf5d-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="ecf5d-113">Voici ce qu’il se passe pendant l’activation de la fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="ecf5d-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="ecf5d-114">Un compte d’ordinateur nommé `AZUREADSSOACCT` (c’est-à-dire Azure AD) est créé dans votre instance Active Directory (AD) locale.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="ecf5d-115">La clé de déchiffrement Kerberos du compte d’ordinateur est partagée en toute sécurité avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="ecf5d-116">Par ailleurs, deux noms de principal du service (SPN) Kerberos sont créés pour représenter les deux URL utilisées pendant la connexion à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="ecf5d-117">Le compte d’ordinateur et les SPN Kerberos sont créés dans chaque forêt AD que vous synchronisez avec Azure AD (via Azure AD Connect) et pour les utilisateurs qui doivent bénéficier de l’authentification unique transparente.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="ecf5d-118">Déplacez le compte d’ordinateur `AZUREADSSOACCT` vers une unité d’organisation (UO) où d’autres comptes d’ordinateurs sont stockés. Vous serez ainsi assuré qu’il sera géré de la même façon et qu’il ne sera pas supprimé.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ecf5d-119">Il est fortement recommandé que vous [substituiez la clé de déchiffrement Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) du `AZUREADSSOACCT` compte d’ordinateur au moins tous les 30 jours.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="ecf5d-120">Comment s’opère une connexion avec l’authentification unique transparente ?</span><span class="sxs-lookup"><span data-stu-id="ecf5d-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="ecf5d-121">Une fois la configuration terminée, l’authentification unique transparente fonctionne de la même façon que n’importe quelle autre connexion utilisant l’authentification Windows intégrée (IWA).</span><span class="sxs-lookup"><span data-stu-id="ecf5d-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="ecf5d-122">Voici comment se déroule l’opération :</span><span class="sxs-lookup"><span data-stu-id="ecf5d-122">The flow is as follows:</span></span>

1. <span data-ttu-id="ecf5d-123">Un utilisateur tente d’accéder à une application (par exemple, Outlook Web App - https://outlook.office365.com/owa/) à partir d’un appareil d’entreprise joint à un domaine au sein du réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="ecf5d-124">Si l’utilisateur n’est pas déjà connecté, il est redirigé vers la page de connexion Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="ecf5d-125">Si la demande de connexion Azure AD inclut un paramètre `domain_hint` (identifiant votre locataire, par exemple contoso.onmicrosoft.com) ou un paramètre `login_hint` (identifiant l’utilisateur, par exemple user@contoso.onmicrosoft.com ou user@contoso.com), l’étape 2 est ignorée.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="ecf5d-126">L’utilisateur tape son nom d’utilisateur dans la page de connexion Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="ecf5d-127">En utilisant JavaScript en arrière-plan, Azure AD demande au client, via une réponse 401 Non autorisé, de fournir un ticket Kerberos.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="ecf5d-128">À son tour, le navigateur demande un ticket à Active Directory pour le compte d’ordinateur `AZUREADSSOACCT` (qui représente Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecf5d-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="ecf5d-129">Active Directory localise le compte d’ordinateur et retourne un ticket Kerberos au navigateur chiffré avec le secret du compte d’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="ecf5d-130">Le navigateur transmet le ticket Kerberos qu’il a acquis auprès d’Active Directory à Azure AD (à l’une des [URL Azure AD précédemment ajoutées aux paramètres Zone intranet du navigateur](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="ecf5d-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="ecf5d-131">Azure AD déchiffre le ticket Kerberos, qui comprend l’identité de l’utilisateur connecté à l’appareil d’entreprise, en utilisant la clé partagée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="ecf5d-132">À l’issue de l’évaluation, Azure AD retourne un jeton à l’application ou bien demande à l’utilisateur de fournir des preuves supplémentaires, telles qu’une authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="ecf5d-133">Si l’utilisateur parvient à se connecter, il peut accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="ecf5d-134">Le schéma suivant illustre tous les composants et les étapes impliquées dans ce processus.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-134">The following diagram illustrates all the components and the steps involved.</span></span>

![Authentification unique transparente](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="ecf5d-136">L’authentification unique transparente est opportuniste, ce qui signifie que si elle échoue, l’expérience de connexion reprend son comportement normal (l’utilisateur doit entrer son mot de passe pour se connecter).</span><span class="sxs-lookup"><span data-stu-id="ecf5d-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecf5d-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ecf5d-137">Next steps</span></span>

- <span data-ttu-id="ecf5d-138">[**Démarrage rapide**](active-directory-aadconnect-sso-quick-start.md) : mettez en service l’authentification unique transparente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="ecf5d-139">[**Questions fréquentes (FAQ)**](active-directory-aadconnect-sso-faq.md) : réponses aux questions fréquentes.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="ecf5d-140">[**Résolution des problèmes**](active-directory-aadconnect-troubleshoot-sso.md) : découvrez comment résoudre les problèmes courants susceptibles de survenir avec cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="ecf5d-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour le dépôt de nouvelles demandes de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="ecf5d-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
