---
title: 'Azure AD Connect : authentification directe - Limitations actuelles | Microsoft Docs'
description: "Cet article décrit les limitations actuelles de hello d’authentification de pass-through Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
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
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="b70d5-104">Authentification directe Azure Active Directory : limitations actuelles</span><span class="sxs-lookup"><span data-stu-id="b70d5-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="b70d5-105">L’authentification directe Azure AD est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="b70d5-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="b70d5-106">Il s’agit d’une fonctionnalité gratuite et vous n’avez pas besoin des éditions payantes d’Azure AD toouse il.</span><span class="sxs-lookup"><span data-stu-id="b70d5-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="b70d5-107">Authentification directe est uniquement disponible dans hello world-wide instance d’Azure AD et non sous [Microsoft Cloud Allemagne](http://www.microsoft.de/cloud-deutschland) et [Cloud de Microsoft Azure Government](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="b70d5-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="b70d5-108">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="b70d5-108">Supported scenarios</span></span>

<span data-ttu-id="b70d5-109">Hello les scénarios suivants est entièrement pris en charge pendant l’aperçu :</span><span class="sxs-lookup"><span data-stu-id="b70d5-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="b70d5-110">L’utilisateur se connecte dans toutes les applications basées sur un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b70d5-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="b70d5-111">L’utilisateur se connecte dans les applications clientes Office 365 prenant en charge [l’authentification moderne](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="b70d5-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="b70d5-112">Azure AD Join pour les appareils Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b70d5-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="b70d5-113">Prise en charge d’Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="b70d5-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="b70d5-114">Scénarios non pris en charge</span><span class="sxs-lookup"><span data-stu-id="b70d5-114">Unsupported scenarios</span></span>

<span data-ttu-id="b70d5-115">Hello scénarios suivants sont _pas_ pris en charge pendant l’aperçu :</span><span class="sxs-lookup"><span data-stu-id="b70d5-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="b70d5-116">Connexions des utilisateurs dans les applications clientes Office héritées (Office 2013 ou version antérieure).</span><span class="sxs-lookup"><span data-stu-id="b70d5-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="b70d5-117">Les organisations sont encouragés tooswitch toomodern authentification, si possible.</span><span class="sxs-lookup"><span data-stu-id="b70d5-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="b70d5-118">L’authentification moderne permet non seulement de prendre en charge l’authentification directe, mais également de sécuriser les comptes d’utilisateur à l’aide des fonctionnalités [d’accès conditionnel](../active-directory-conditional-access.md), comme l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="b70d5-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="b70d5-119">Connexions des utilisateurs à des applications clientes Skype Entreprise, y compris Skype Entreprise 2016.</span><span class="sxs-lookup"><span data-stu-id="b70d5-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="b70d5-120">L’utilisateur se connecte dans PowerShell v1.0.</span><span class="sxs-lookup"><span data-stu-id="b70d5-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="b70d5-121">Il est recommandé d’utiliser à la place PowerShell v2.0.</span><span class="sxs-lookup"><span data-stu-id="b70d5-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b70d5-122">Comme solution de contournement pour les scénarios non pris en charge, activez la synchronisation du hachage de mot de passe sur hello [fonctionnalités facultatives](active-directory-aadconnect-get-started-custom.md#optional-features) page dans l’Assistant de connexion hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b70d5-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="b70d5-123">Synchronisation du hachage de mot de passe joue le rôle de secours pour hello précédant les scénarios _uniquement_ (et _pas_ comme une générique tooPass via l’authentification de secours).</span><span class="sxs-lookup"><span data-stu-id="b70d5-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="b70d5-124">Si vous n’avez pas besoin de ces scénarios, désactivez la synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b70d5-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b70d5-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b70d5-125">Next steps</span></span>
- <span data-ttu-id="b70d5-126">[**Démarrage rapide**](active-directory-aadconnect-pass-through-authentication-quick-start.md) : Mise en route de l’authentification directe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b70d5-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="b70d5-127">[**Immersion technique**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b70d5-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="b70d5-128">[**Forum aux Questions** ](active-directory-aadconnect-pass-through-authentication-faq.md) -réponses elles sonttrop aux questions.</span><span class="sxs-lookup"><span data-stu-id="b70d5-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="b70d5-129">[**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="b70d5-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="b70d5-130">[**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.</span><span class="sxs-lookup"><span data-stu-id="b70d5-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="b70d5-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="b70d5-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
