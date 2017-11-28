---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer les besoins de l’authentification multifacteur"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello que vous choisissez lors de l’authentification utilisateur de hello et avant d’autoriser l’accès toohello application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="e6b95-104">Déterminer les besoins d'authentification multifacteur (Multi-Factor Authentication) pour votre solution d'identités hybrides</span><span class="sxs-lookup"><span data-stu-id="e6b95-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="e6b95-105">Dans ce monde de mobilité, avec les utilisateurs qui accèdent aux données et des applications dans le cloud de hello et à partir de n’importe quel appareil, sécuriser ces informations jouent un rôle essentiel.</span><span class="sxs-lookup"><span data-stu-id="e6b95-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="e6b95-106">On entend parler chaque jour de nouvelles failles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="e6b95-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="e6b95-107">Bien qu’il n’existe aucune garantie contre ces violations, l’authentification multifacteur, fournit une couche supplémentaire de sécurité toohelp empêcher les violations.</span><span class="sxs-lookup"><span data-stu-id="e6b95-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="e6b95-108">Commencez par l’évaluation des besoins des entreprises hello pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="e6b95-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="e6b95-109">Autrement dit, ce qui est toosecure lors de la tentative de hello entreprise.</span><span class="sxs-lookup"><span data-stu-id="e6b95-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="e6b95-110">Cette évaluation est important toodefine hello technique configuration requise pour installer et activer les utilisateurs des organisations hello pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="e6b95-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="e6b95-111">Si vous n’êtes pas familiarisé avec l’authentification Multifacteur et ce qu’il fait, il est fortement recommandé de lire l’article de hello [Nouveautés d’Azure multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue préalable lire cette section.</span><span class="sxs-lookup"><span data-stu-id="e6b95-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="e6b95-112">Rendre suivant de hello tooanswer que :</span><span class="sxs-lookup"><span data-stu-id="e6b95-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="e6b95-113">Votre entreprise tente d’applications de Microsoft toosecure ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="e6b95-114">Comment ces applications sont-elles publiées ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-114">How these apps are published?</span></span>
* <span data-ttu-id="e6b95-115">Votre entreprise fournit l’accès à distance tooallow employés tooaccess local applications ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="e6b95-116">Si Oui, quel type d’accès à distance ? Vous devez également tooevaluate où les utilisateurs hello qui accèdent à ces applications se trouve.</span><span class="sxs-lookup"><span data-stu-id="e6b95-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="e6b95-117">Cette évaluation est une autre stratégie de l’authentification multifacteur appropriée hello toodefine étape importante.</span><span class="sxs-lookup"><span data-stu-id="e6b95-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="e6b95-118">Vérifiez que hello tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="e6b95-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e6b95-119">Où sont situés les utilisateurs hello va toobe ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="e6b95-120">Peuvent-ils se trouver à un endroit quelconque ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="e6b95-121">Votre entreprise souhaite-t-elle restrictions tooestablish selon l’emplacement de l’utilisateur toohello ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="e6b95-122">Une fois que vous avez compris ces exigences, il est important de tooalso évaluer les besoins de l’utilisateur hello pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="e6b95-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="e6b95-123">Cette évaluation est importante, car elle définit les exigences de hello pour le déploiement de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="e6b95-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="e6b95-124">Vérifiez que hello tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="e6b95-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e6b95-125">Sont les utilisateurs de hello familiarisé avec l’authentification multifacteur ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="e6b95-126">Certaines utilisations sera une authentification supplémentaire tooprovide requis ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="e6b95-127">Si Oui, toutes les hello moment, provenant des réseaux externes, ou l’accès aux applications spécifiques, ou dans d’autres conditions ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="e6b95-128">Les utilisateurs hello besoin d’une formation sur la façon de toosetup et implémenter l’authentification multifacteur ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="e6b95-129">Quels sont les scénarios clés hello que votre entreprise souhaite tooenable l’authentification multifacteur pour les utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="e6b95-130">Après avoir répondu aux questions précédentes de hello, vous serez en mesure de toounderstand s’il y a déjà mis en œuvre l’authentification multifacteur localement.</span><span class="sxs-lookup"><span data-stu-id="e6b95-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="e6b95-131">Cette évaluation est important toodefine hello technique configuration requise pour installer et activer les utilisateurs des organisations hello pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="e6b95-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="e6b95-132">Vérifiez que hello tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="e6b95-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e6b95-133">Votre entreprise a-t-elle besoin de comptes tooprotect privilégié avec l’authentification Multifacteur ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="e6b95-134">Votre entreprise a-t-elle besoin tooenable l’authentification Multifacteur pour certaines applications pour des raisons de conformité ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="e6b95-135">Votre entreprise a-t-elle besoin tooenable l’authentification Multifacteur pour tous les utilisateurs de ces applications ou les seuls les administrateurs ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="e6b95-136">Peut-être avez-vous MFA toujours activée ou uniquement lorsque les utilisateurs de hello sont enregistrés en dehors de votre réseau d’entreprise ?</span><span class="sxs-lookup"><span data-stu-id="e6b95-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6b95-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6b95-137">Next steps</span></span>
[<span data-ttu-id="e6b95-138">Définir une stratégie d’adoption des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="e6b95-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="e6b95-139">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e6b95-139">See also</span></span>
[<span data-ttu-id="e6b95-140">Présentation des considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="e6b95-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

