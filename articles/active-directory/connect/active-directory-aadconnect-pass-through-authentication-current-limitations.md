---
title: 'Azure AD Connect : authentification directe - Limitations actuelles | Microsoft Docs'
description: "Cet article décrit les limitations actuelles de l’authentification directe Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="fee13-104">Authentification directe Azure Active Directory : limitations actuelles</span><span class="sxs-lookup"><span data-stu-id="fee13-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="fee13-105">L’authentification directe Azure AD est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="fee13-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="fee13-106">Cette fonctionnalité est gratuite et il est inutile de disposer des éditions payantes d’Azure AD pour l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="fee13-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="fee13-107">L’authentification directe est disponible seulement dans l’instance mondiale d’Azure AD, et pas sur [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) ni sur [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="fee13-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="fee13-108">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="fee13-108">Supported scenarios</span></span>

<span data-ttu-id="fee13-109">Les scénarios suivants sont entièrement pris en charge dans la version préliminaire :</span><span class="sxs-lookup"><span data-stu-id="fee13-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="fee13-110">L’utilisateur se connecte dans toutes les applications basées sur un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="fee13-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="fee13-111">L’utilisateur se connecte dans les applications clientes Office 365 prenant en charge [l’authentification moderne](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="fee13-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="fee13-112">Azure AD Join pour les appareils Windows 10.</span><span class="sxs-lookup"><span data-stu-id="fee13-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="fee13-113">Prise en charge d’Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="fee13-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="fee13-114">Scénarios non pris en charge</span><span class="sxs-lookup"><span data-stu-id="fee13-114">Unsupported scenarios</span></span>

<span data-ttu-id="fee13-115">Les scénarios suivants ne sont _pas_ pris en charge dans la version préliminaire :</span><span class="sxs-lookup"><span data-stu-id="fee13-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="fee13-116">Connexions des utilisateurs dans les applications clientes Office héritées (Office 2013 ou version antérieure).</span><span class="sxs-lookup"><span data-stu-id="fee13-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="fee13-117">Nous recommandons aux entreprises de basculer si possible vers l’authentification moderne.</span><span class="sxs-lookup"><span data-stu-id="fee13-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="fee13-118">L’authentification moderne permet non seulement de prendre en charge l’authentification directe, mais également de sécuriser les comptes d’utilisateur à l’aide des fonctionnalités [d’accès conditionnel](../active-directory-conditional-access.md), comme l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="fee13-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="fee13-119">Connexions des utilisateurs à des applications clientes Skype Entreprise, y compris Skype Entreprise 2016.</span><span class="sxs-lookup"><span data-stu-id="fee13-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="fee13-120">L’utilisateur se connecte dans PowerShell v1.0.</span><span class="sxs-lookup"><span data-stu-id="fee13-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="fee13-121">Il est recommandé d’utiliser à la place PowerShell v2.0.</span><span class="sxs-lookup"><span data-stu-id="fee13-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fee13-122">Comme solution de contournement pour les scénarios non pris en charge, activez la synchronisation du hachage de mot de passe sur la page [Fonctionnalités facultatives](active-directory-aadconnect-get-started-custom.md#optional-features) dans l’Assistant Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="fee13-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="fee13-123">La synchronisation du hachage de mot de passe agit comme solution de secours _uniquement_ pour les scénarios précédents (et _non pas_ comme solution de secours générique pour l’authentification directe).</span><span class="sxs-lookup"><span data-stu-id="fee13-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="fee13-124">Si vous n’avez pas besoin de ces scénarios, désactivez la synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="fee13-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fee13-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fee13-125">Next steps</span></span>
- <span data-ttu-id="fee13-126">[**Démarrage rapide**](active-directory-aadconnect-pass-through-authentication-quick-start.md) : Mise en route de l’authentification directe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fee13-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="fee13-127">[**Immersion technique**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fee13-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="fee13-128">[**Forum aux questions**](active-directory-aadconnect-pass-through-authentication-faq.md) : réponses aux questions fréquentes.</span><span class="sxs-lookup"><span data-stu-id="fee13-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="fee13-129">[**Résolution des problèmes**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) : découvrez comment résoudre les problèmes courants susceptibles de se produire avec cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fee13-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="fee13-130">[**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.</span><span class="sxs-lookup"><span data-stu-id="fee13-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="fee13-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="fee13-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
