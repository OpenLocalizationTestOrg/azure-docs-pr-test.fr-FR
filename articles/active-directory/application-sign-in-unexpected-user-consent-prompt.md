---
title: "Invite de consentement inattendue lors de la connexion à une application | Microsoft Docs"
description: "Procédure de dépannage à suivre quand un utilisateur voit une invite de consentement inattendue pour une application intégrée à Azure AD"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="d5de3-103">Invite de consentement inattendue lors de la connexion à une application</span><span class="sxs-lookup"><span data-stu-id="d5de3-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="d5de3-104">Pour s’exécuter, de nombreuses applications qui s’intègrent à Azure Active Directory nécessitent des autorisations à plusieurs ressources.</span><span class="sxs-lookup"><span data-stu-id="d5de3-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="d5de3-105">Quand ces ressources sont également intégrées à Azure Active Directory, vous devez utiliser l’infrastructure de consentement Azure AD pour demander les autorisations nécessaires pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="d5de3-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="d5de3-106">Une invite de consentement est alors affichée à la première utilisation d’une application (il s’agit généralement d’une opération unique).</span><span class="sxs-lookup"><span data-stu-id="d5de3-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="d5de3-107">Scénarios dans lesquels des invites de consentement sont présentées aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d5de3-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="d5de3-108">Divers scénarios entraînent l’affichage d’invites supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="d5de3-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="d5de3-109">Le jeu d’autorisations exigées par l’application a changé.</span><span class="sxs-lookup"><span data-stu-id="d5de3-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="d5de3-110">L’utilisateur ayant initialement donné son consentement à l’application n’était pas un administrateur, et un autre utilisateur (non-administrateur) utilise l’application pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="d5de3-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="d5de3-111">L’utilisateur ayant initialement donné son consentement à l’application était un administrateur, mais il n’a pas donné son consentement au nom de toute l’organisation.</span><span class="sxs-lookup"><span data-stu-id="d5de3-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="d5de3-112">L’application utilise le [consentement incrémentiel et dynamique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) pour demander des autorisations supplémentaires après le consentement initial.</span><span class="sxs-lookup"><span data-stu-id="d5de3-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="d5de3-113">Ce cas de figure se présente souvent quand les fonctionnalités facultatives d’une application nécessitent des autorisations au-delà de celles exigées pour les fonctionnalités de base.</span><span class="sxs-lookup"><span data-stu-id="d5de3-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="d5de3-114">Le consentement, bien qu’initialement accordé, a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="d5de3-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="d5de3-115">Le développeur a configuré l’application pour exiger une invite de consentement à chaque utilisation (ce qui n’est pas recommandé).</span><span class="sxs-lookup"><span data-stu-id="d5de3-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5de3-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d5de3-116">Next steps</span></span>

-   [<span data-ttu-id="d5de3-117">Applications, autorisations et consentement dans Azure Active Directory (point de terminaison v1.0)</span><span class="sxs-lookup"><span data-stu-id="d5de3-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="d5de3-118">Étendues, autorisations et consentement dans Azure Active Directory (point de terminaison v2.0)</span><span class="sxs-lookup"><span data-stu-id="d5de3-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


