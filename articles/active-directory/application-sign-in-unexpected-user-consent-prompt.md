---
title: "invite de consentement aaaUnexpected pour se connecter à l’application de tooan | Documents Microsoft"
description: "Comment tootroubleshoot lorsqu’un utilisateur voit une invite de consentement pour une application que vous avez intégré à Azure AD que vous n’avez pas prévues"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="650f8-103">Invite de consentement inattendue lors de la connexion tooan application</span><span class="sxs-lookup"><span data-stu-id="650f8-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="650f8-104">De nombreuses applications qui s’intègrent à Azure Active Directory nécessitent des ressources autorisations toovarious toorun d’ordre.</span><span class="sxs-lookup"><span data-stu-id="650f8-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="650f8-105">Lorsque ces ressources sont également intégrées dans Azure Active Directory, tooaccess autorisations leur est demandé à l’aide d’Azure AD de hello consentement framework.</span><span class="sxs-lookup"><span data-stu-id="650f8-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="650f8-106">Cela entraîne une invite de consentement affichée hello première fois, qu'une application est utilisée, ce qui est souvent une opération unique.</span><span class="sxs-lookup"><span data-stu-id="650f8-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="650f8-107">Scénarios dans lesquels des invites de consentement sont présentées aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="650f8-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="650f8-108">Divers scénarios entraînent l’affichage d’invites supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="650f8-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="650f8-109">ensemble de Hello des autorisations requises par l’application hello ont été modifiés.</span><span class="sxs-lookup"><span data-stu-id="650f8-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="650f8-110">utilisateur Hello qui a donné son consentement à l’origine des toohello application n’était pas un administrateur, et désormais un utilisateur différent (non-admin) utilise application hello pour hello première fois.</span><span class="sxs-lookup"><span data-stu-id="650f8-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="650f8-111">utilisateur Hello qui a donné son consentement à l’origine des toohello application était un administrateur, mais elles ne pas consentement à la place de l’ensemble de l’organisation hello.</span><span class="sxs-lookup"><span data-stu-id="650f8-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="650f8-112">à l’aide d’application Hello [consentement incrémentielle et dynamique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest des autorisations supplémentaires une fois le consentement a été initialement accordé.</span><span class="sxs-lookup"><span data-stu-id="650f8-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="650f8-113">Ce cas de figure se présente souvent quand les fonctionnalités facultatives d’une application nécessitent des autorisations au-delà de celles exigées pour les fonctionnalités de base.</span><span class="sxs-lookup"><span data-stu-id="650f8-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="650f8-114">Le consentement, bien qu’initialement accordé, a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="650f8-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="650f8-115">développeur de Hello a configuré hello application toorequire une invite de consentement chaque fois qu’elle est utilisée (Remarque : cela n’est pas recommandé).</span><span class="sxs-lookup"><span data-stu-id="650f8-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="650f8-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="650f8-116">Next steps</span></span>

-   [<span data-ttu-id="650f8-117">Applications, autorisations et consentement dans Azure Active Directory (point de terminaison v1.0)</span><span class="sxs-lookup"><span data-stu-id="650f8-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="650f8-118">Les étendues, les autorisations et consentement Bonjour Azure Active Directory (point de terminaison v2.0)</span><span class="sxs-lookup"><span data-stu-id="650f8-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


