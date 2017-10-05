---
title: "Forum aux questions sur l’accès conditionnel Azure Active Directory | Microsoft Docs"
description: "Trouvez les réponses aux questions les plus fréquentes sur l’accès conditionnel dans Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="29eab-103">Forum aux questions sur l’accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29eab-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="29eab-104">A quelles applications les stratégies d’accès conditionnel s’appliquent-elles ?</span><span class="sxs-lookup"><span data-stu-id="29eab-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="29eab-105">Pour plus d’informations sur les applications qui fonctionnent avec les stratégies d’accès conditionnel, consultez [Applications et navigateurs qui utilisent des règles d’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="29eab-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="29eab-106">Les stratégies d’accès conditionnel s’appliquent-elles à la collaboration B2B et aux utilisateurs invités ?</span><span class="sxs-lookup"><span data-stu-id="29eab-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="29eab-107">Les stratégies sont appliquées aux utilisateurs dans le cadre d’une collaboration business-to-business (B2B).</span><span class="sxs-lookup"><span data-stu-id="29eab-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="29eab-108">Toutefois, dans certains cas, un utilisateur peut ne pas être en mesure de satisfaire aux exigences de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="29eab-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="29eab-109">Par exemple, il est possible que l’organisation d’un utilisateur invité ne prenne pas en charge l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="29eab-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="29eab-110">La stratégie SharePoint Online s’applique-t-elle également à OneDrive Entreprise ?</span><span class="sxs-lookup"><span data-stu-id="29eab-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="29eab-111">Oui.</span><span class="sxs-lookup"><span data-stu-id="29eab-111">Yes.</span></span> <span data-ttu-id="29eab-112">Une stratégie SharePoint Online s’applique également à OneDrive Entreprise.</span><span class="sxs-lookup"><span data-stu-id="29eab-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="29eab-113">Pourquoi ne puis-je pas définir une stratégie pour les applications clientes telles que Word ou Outlook ?</span><span class="sxs-lookup"><span data-stu-id="29eab-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="29eab-114">Une stratégie d’accès conditionnel définit les conditions requises pour accéder à un service.</span><span class="sxs-lookup"><span data-stu-id="29eab-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="29eab-115">Elle est appliquée quand l’authentification à ce service a lieu.</span><span class="sxs-lookup"><span data-stu-id="29eab-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="29eab-116">La stratégie n’est pas définie directement sur une application cliente.</span><span class="sxs-lookup"><span data-stu-id="29eab-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="29eab-117">Au lieu de cela, elle est appliquée quand un client appelle un service.</span><span class="sxs-lookup"><span data-stu-id="29eab-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="29eab-118">Par exemple, une stratégie définie sur SharePoint s’applique aux clients qui appellent SharePoint.</span><span class="sxs-lookup"><span data-stu-id="29eab-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="29eab-119">Une stratégie définie sur Exchange s’applique à Outlook.</span><span class="sxs-lookup"><span data-stu-id="29eab-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="29eab-120">La stratégie d’accès conditionnel s’applique-t-elle aux comptes de service ?</span><span class="sxs-lookup"><span data-stu-id="29eab-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="29eab-121">Les stratégies d’accès conditionnel s’appliquent à tous les comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29eab-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="29eab-122">Cela inclut les comptes d’utilisateur utilisés comme comptes de service.</span><span class="sxs-lookup"><span data-stu-id="29eab-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="29eab-123">Souvent, un compte de service qui s’exécute sans assistance ne peut pas répondre aux exigences d’une stratégie d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="29eab-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="29eab-124">Par exemple, l’authentification multifacteur peut être obligatoire.</span><span class="sxs-lookup"><span data-stu-id="29eab-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="29eab-125">Les comptes de service peuvent être exclus d’une stratégie à l’aide des paramètres de gestion de stratégie d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="29eab-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="29eab-126">Des API graphiques sont-elles disponibles pour la configuration des stratégies d’accès conditionnel ?</span><span class="sxs-lookup"><span data-stu-id="29eab-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="29eab-127">Actuellement, non.</span><span class="sxs-lookup"><span data-stu-id="29eab-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="29eab-128">Quelle est la stratégie d’exclusion par défaut pour les plateformes d’appareils non prises en charge ?</span><span class="sxs-lookup"><span data-stu-id="29eab-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="29eab-129">À l’heure actuelle, les stratégies d’accès conditionnel sont appliquées de manière sélective aux utilisateurs d’appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="29eab-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="29eab-130">Les applications sur d’autres plateformes d’appareils ne sont pas, par défaut, affectées par la stratégie d’accès conditionnel pour appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="29eab-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="29eab-131">Un administrateur de locataires peut choisir de remplacer la stratégie globale pour interdire l’accès aux utilisateurs sur des plateformes non prises en charge.</span><span class="sxs-lookup"><span data-stu-id="29eab-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="29eab-132">Comment les stratégies d’accès conditionnel fonctionnent-elles pour Microsoft Teams ?</span><span class="sxs-lookup"><span data-stu-id="29eab-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="29eab-133">Microsoft Teams s’appuie fortement sur Exchange Online et SharePoint Online pour les principaux scénarios de productivité, tels que les réunions, les calendriers et le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="29eab-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="29eab-134">Les stratégies d’accès conditionnel définies pour ces applications cloud s’appliquent à Microsoft Teams quand un utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="29eab-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="29eab-135">Microsoft Teams est également pris en charge séparément en tant qu’application cloud dans les stratégies d’accès conditionnel Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29eab-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="29eab-136">Les stratégies d’autorité de certification définies pour ces applications cloud s’appliquent à Microsoft Teams quand un utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="29eab-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="29eab-137">Les clients de bureau Microsoft Teams pour Windows et Mac prennent en charge l’authentification moderne.</span><span class="sxs-lookup"><span data-stu-id="29eab-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="29eab-138">L’authentification moderne permet d’utiliser la connexion basée sur la bibliothèque ADAL (Azure Active Directory Authentication Library) pour les applications clientes Microsoft Office sur plusieurs plateformes.</span><span class="sxs-lookup"><span data-stu-id="29eab-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 