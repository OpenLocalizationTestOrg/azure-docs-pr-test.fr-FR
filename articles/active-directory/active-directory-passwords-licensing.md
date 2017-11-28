---
title: "Liences : réinitialisation de mot de passe en libre-service Azure AD | Microsoft Docs"
description: "Conditions de licence pour la réinitialisation du mot de passe en libre-service dans Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="bd864-103">Conditions de licence pour la réinitialisation du mot de passe en libre-service Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd864-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="bd864-104">Dans l’ordre pour toofunction de réinitialisation de mot de passe Azure AD, vous **doit disposer d’au moins une licence de votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="bd864-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="bd864-105">Nous n’imposent pas de gestionnaire de licences sur l’expérience de réinitialisation de mot de passe hello par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bd864-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="bd864-106">conformité toomaintain avec votre contrat de licence de Microsoft, vous devez tooassign licences tooany utilisateurs qui utilisent les fonctionnalités premium.</span><span class="sxs-lookup"><span data-stu-id="bd864-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="bd864-107">**Utilisateurs du cloud uniquement** : n’importe quelle référence Office 365 (O365) payante ou Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="bd864-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="bd864-108">Utilisateurs **cloud** et/ou **locaux** : Azure AD Premium P1 ou P2, Enterprise Mobility + Security (EMS) ou Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="bd864-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="bd864-109">Licences requises pour la réécriture du mot de passe</span><span class="sxs-lookup"><span data-stu-id="bd864-109">Licenses required for password writeback</span></span>

<span data-ttu-id="bd864-110">l’écriture différée de mot de passe toouse, vous devez avoir un de hello suivant licences attribuées dans votre client.</span><span class="sxs-lookup"><span data-stu-id="bd864-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="bd864-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="bd864-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="bd864-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="bd864-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="bd864-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="bd864-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="bd864-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="bd864-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="bd864-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="bd864-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="bd864-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="bd864-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="bd864-117">Autonome Office 365 régimes de licences **ne prennent pas en charge l’écriture différée de mot de passe** et exiger de hello précédant les plans pour toowork de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bd864-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="bd864-118">Les informations de licence supplémentaires, y compris les coûts se trouvent sur hello suivant des pages</span><span class="sxs-lookup"><span data-stu-id="bd864-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="bd864-119">Site de tarification d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd864-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="bd864-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="bd864-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="bd864-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="bd864-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="bd864-122">Activer les licences utilisateur ou groupe</span><span class="sxs-lookup"><span data-stu-id="bd864-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="bd864-123">Azure AD prend en charge basée sur le groupe de licences des licences de tooassign permettant aux administrateurs dans tooa groupe d’utilisateurs, plutôt que leur attribuer une à la fois.</span><span class="sxs-lookup"><span data-stu-id="bd864-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="bd864-124">Affecter, vérifier et résoudre les problèmes de licences</span><span class="sxs-lookup"><span data-stu-id="bd864-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="bd864-125">Certains services Microsoft ne sont pas disponibles dans tous les emplacements.</span><span class="sxs-lookup"><span data-stu-id="bd864-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="bd864-126">Avant tooa utilisateur peut être affectée à une licence, administrateur de hello doit spécifier des propriétés de « Emplacement d’utilisation » hello sur utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="bd864-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="bd864-127">Attribution de licences peut être effectuée sous utilisateur > profil > section des paramètres de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd864-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="bd864-128">**Lorsque vous utilisez l’attribution de licence de groupe, tous les utilisateurs sans un emplacement d’utilisation spécifié héritent emplacement hello du répertoire de hello.**</span><span class="sxs-lookup"><span data-stu-id="bd864-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd864-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd864-129">Next steps</span></span>

<span data-ttu-id="bd864-130">Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd864-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="bd864-131">[**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd864-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="bd864-132">[**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe</span><span class="sxs-lookup"><span data-stu-id="bd864-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="bd864-133">[**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici</span><span class="sxs-lookup"><span data-stu-id="bd864-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="bd864-134">[**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="bd864-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="bd864-135">[**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="bd864-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="bd864-136">[**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement</span><span class="sxs-lookup"><span data-stu-id="bd864-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="bd864-137">[**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ?</span><span class="sxs-lookup"><span data-stu-id="bd864-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="bd864-138">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="bd864-138">Why?</span></span> <span data-ttu-id="bd864-139">Quoi ?</span><span class="sxs-lookup"><span data-stu-id="bd864-139">What?</span></span> <span data-ttu-id="bd864-140">Où ?</span><span class="sxs-lookup"><span data-stu-id="bd864-140">Where?</span></span> <span data-ttu-id="bd864-141">Qui ?</span><span class="sxs-lookup"><span data-stu-id="bd864-141">Who?</span></span> <span data-ttu-id="bd864-142">Quand ?</span><span class="sxs-lookup"><span data-stu-id="bd864-142">When?</span></span> <span data-ttu-id="bd864-143">-Réponses tooquestions vous souhaitiez toujours tooask</span><span class="sxs-lookup"><span data-stu-id="bd864-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="bd864-144">[**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR</span><span class="sxs-lookup"><span data-stu-id="bd864-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

