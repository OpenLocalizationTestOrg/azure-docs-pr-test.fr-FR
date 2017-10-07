---
title: "aaaAzure Active Directory un accès conditionnel FAQ | Documents Microsoft"
description: "Obtenir elles sonttrop des réponses aux questions sur l’accès conditionnel dans Azure Active Directory."
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
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="9e54b-103">Forum aux questions sur l’accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e54b-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="9e54b-104">A quelles applications les stratégies d’accès conditionnel s’appliquent-elles ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="9e54b-105">Pour plus d’informations sur les applications qui fonctionnent avec les stratégies d’accès conditionnel, consultez [Applications et navigateurs qui utilisent des règles d’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9e54b-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="9e54b-106">Les stratégies d’accès conditionnel s’appliquent-elles à la collaboration B2B et aux utilisateurs invités ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="9e54b-107">Les stratégies sont appliquées aux utilisateurs dans le cadre d’une collaboration business-to-business (B2B).</span><span class="sxs-lookup"><span data-stu-id="9e54b-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="9e54b-108">Toutefois, dans certains cas, un utilisateur ne peut pas être exigences hello toosatisfy en mesure de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e54b-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="9e54b-109">Par exemple, il est possible que l’organisation d’un utilisateur invité ne prenne pas en charge l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="9e54b-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="9e54b-110">Une stratégie SharePoint Online également applique-t-elle tooOneDrive for Business ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="9e54b-111">Oui.</span><span class="sxs-lookup"><span data-stu-id="9e54b-111">Yes.</span></span> <span data-ttu-id="9e54b-112">Une stratégie SharePoint Online s’applique également tooOneDrive for Business.</span><span class="sxs-lookup"><span data-stu-id="9e54b-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="9e54b-113">Pourquoi ne puis-je pas définir une stratégie pour les applications clientes telles que Word ou Outlook ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="9e54b-114">Une stratégie d’accès conditionnel définit les conditions requises pour accéder à un service.</span><span class="sxs-lookup"><span data-stu-id="9e54b-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="9e54b-115">Elle est appliquée lorsque le service d’authentification toothat se produit.</span><span class="sxs-lookup"><span data-stu-id="9e54b-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="9e54b-116">stratégie de Hello n’est pas définie directement sur une application cliente.</span><span class="sxs-lookup"><span data-stu-id="9e54b-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="9e54b-117">Au lieu de cela, elle est appliquée quand un client appelle un service.</span><span class="sxs-lookup"><span data-stu-id="9e54b-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="9e54b-118">Par exemple, une stratégie définie sur SharePoint applique tooclients appel de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9e54b-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="9e54b-119">Une stratégie définie sur Exchange applique tooOutlook.</span><span class="sxs-lookup"><span data-stu-id="9e54b-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="9e54b-120">Une stratégie d’accès conditionnel s’applique tooservice comptes ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="9e54b-121">Stratégies d’accès conditionnel s’appliquent à des comptes d’utilisateur tooall.</span><span class="sxs-lookup"><span data-stu-id="9e54b-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="9e54b-122">Cela inclut les comptes d’utilisateur utilisés comme comptes de service.</span><span class="sxs-lookup"><span data-stu-id="9e54b-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="9e54b-123">Souvent, un compte de service qui s’exécute sans assistance ne peut pas satisfaire les exigences de hello d’une stratégie d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="9e54b-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="9e54b-124">Par exemple, l’authentification multifacteur peut être obligatoire.</span><span class="sxs-lookup"><span data-stu-id="9e54b-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="9e54b-125">Les comptes de service peuvent être exclus d’une stratégie à l’aide des paramètres de gestion de stratégie d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="9e54b-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="9e54b-126">Des API graphiques sont-elles disponibles pour la configuration des stratégies d’accès conditionnel ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="9e54b-127">Actuellement, non.</span><span class="sxs-lookup"><span data-stu-id="9e54b-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="9e54b-128">Qu’est la stratégie d’exclusion par défaut hello pour les plateformes d’appareils non pris en charge ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="9e54b-129">À l’heure actuelle, les stratégies d’accès conditionnel sont appliquées de manière sélective aux utilisateurs d’appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="9e54b-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="9e54b-130">Les applications sur d’autres plateformes d’appareils sont, par défaut, pas affectées par la stratégie d’accès conditionnel hello pour les appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="9e54b-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="9e54b-131">Un administrateur client peut choisir toooverride hello stratégie globale toodisallow accès toousers sur les plateformes qui ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9e54b-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="9e54b-132">Comment les stratégies d’accès conditionnel fonctionnent-elles pour Microsoft Teams ?</span><span class="sxs-lookup"><span data-stu-id="9e54b-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="9e54b-133">Microsoft Teams s’appuie fortement sur Exchange Online et SharePoint Online pour les principaux scénarios de productivité, tels que les réunions, les calendriers et le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="9e54b-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="9e54b-134">Stratégies d’accès conditionnel qui sont définies pour ces applications cloud s’appliquent tooMicrosoft équipes lorsqu’un utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="9e54b-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="9e54b-135">Microsoft Teams est également pris en charge séparément en tant qu’application cloud dans les stratégies d’accès conditionnel Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e54b-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="9e54b-136">Stratégies d’autorité de certificat sont définies pour une application cloud s’appliquent tooMicrosoft équipes lorsqu’un utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="9e54b-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="9e54b-137">Les clients de bureau Microsoft Teams pour Windows et Mac prennent en charge l’authentification moderne.</span><span class="sxs-lookup"><span data-stu-id="9e54b-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="9e54b-138">L’authentification moderne permet connectez-vous basé sur les applications clientes Office hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft sur plusieurs plateformes.</span><span class="sxs-lookup"><span data-stu-id="9e54b-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
