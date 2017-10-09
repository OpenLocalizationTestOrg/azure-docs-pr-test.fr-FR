---
title: "aaaSign dans les expériences avec Azure AD Identity Protection | Documents Microsoft"
description: "Fournit une vue d’ensemble de l’expérience utilisateur hello lors de la Protection de l’identité a atténué ou mis à jour un utilisateur ou lorsque l’authentification multifacteur est requise par une stratégie."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="1d100-104">Expériences de connexion avec Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="1d100-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="1d100-105">Avec Azure Active Directory Identity Protection, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="1d100-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="1d100-106">exiger des utilisateurs tooregister pour l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="1d100-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="1d100-107">gérer les connexions risquées et les utilisateurs compromis</span><span class="sxs-lookup"><span data-stu-id="1d100-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="1d100-108">réponse Hello des problèmes de toothese hello système a un impact sur l’expérience de connexion d’un utilisateur, car il est simplement directement de signature d’en fournissant un nom d’utilisateur et un mot de passe ne sera pas possible plus.</span><span class="sxs-lookup"><span data-stu-id="1d100-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="1d100-109">Des étapes supplémentaires sont requis tooget un utilisateur sauvegarder en toute sécurité dans l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="1d100-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="1d100-110">Cette rubrique donne une vue d’ensemble de l’expérience de connexion d’un utilisateur pour tous les cas qui peuvent se produire.</span><span class="sxs-lookup"><span data-stu-id="1d100-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="1d100-111">**Authentification multifacteur**</span><span class="sxs-lookup"><span data-stu-id="1d100-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="1d100-112">Inscription à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="1d100-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="1d100-113">**Connexion risquée**</span><span class="sxs-lookup"><span data-stu-id="1d100-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="1d100-114">Récupération de connexion à risque</span><span class="sxs-lookup"><span data-stu-id="1d100-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="1d100-115">Connexion à risque bloquée</span><span class="sxs-lookup"><span data-stu-id="1d100-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="1d100-116">Inscription à l’authentification multifacteur au cours d’une connexion à risque</span><span class="sxs-lookup"><span data-stu-id="1d100-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="1d100-117">**Utilisateur à risque**</span><span class="sxs-lookup"><span data-stu-id="1d100-117">**User at risk**</span></span>

* <span data-ttu-id="1d100-118">Récupération de compte compromis</span><span class="sxs-lookup"><span data-stu-id="1d100-118">Compromised account recovery</span></span>
* <span data-ttu-id="1d100-119">Compte compromis bloqué</span><span class="sxs-lookup"><span data-stu-id="1d100-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="1d100-120">Inscription à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="1d100-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="1d100-121">Hello meilleure expérience utilisateur pour les deux, hello du flux de récupération de compte compromis et hello de flux de connexion présente des risques, est lorsque hello utilisateur peut les récupérer.</span><span class="sxs-lookup"><span data-stu-id="1d100-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="1d100-122">Si les utilisateurs sont inscrits pour l’authentification multifacteur, qu’il a déjà un numéro de téléphone associé à leur compte qui peut être des défis de sécurité toopass utilisé.</span><span class="sxs-lookup"><span data-stu-id="1d100-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="1d100-123">Sans intervention du support technique ou l’administrateur aide est toorecover nécessaire à partir de la compromission d’un compte.</span><span class="sxs-lookup"><span data-stu-id="1d100-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="1d100-124">Par conséquent, il est vivement recommandé tooget vos utilisateurs inscrits pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="1d100-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="1d100-125">Les administrateurs peuvent :</span><span class="sxs-lookup"><span data-stu-id="1d100-125">Administrators can:</span></span>

* <span data-ttu-id="1d100-126">définir une stratégie qui impose tooset utilisateurs leurs comptes pour la vérification de sécurité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="1d100-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="1d100-127">Autoriser l’enregistrement de l’authentification multifacteur pour des jours de too30, ignoré au cas où ils souhaitent toogive utilisateurs avant d’inscrire une période de grâce.</span><span class="sxs-lookup"><span data-stu-id="1d100-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="1d100-128">**l’inscription de l’authentification multifacteur Hello comporte trois étapes :**</span><span class="sxs-lookup"><span data-stu-id="1d100-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="1d100-129">Dans la première étape de hello, utilisateur de hello reçoit une notification à propos hello exigence tooset hello du compte pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="1d100-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="1d100-130">![Correction](./media/active-directory-identityprotection-flows/140.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="1d100-131">l’authentification multifacteur tooset haut, il vous faut toolet hello système savoir comment vous souhaitez toobe contacté.</span><span class="sxs-lookup"><span data-stu-id="1d100-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="1d100-132">![Correction](./media/active-directory-identityprotection-flows/141.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="1d100-133">système de Hello soumet une demande d’accès tooyou et que vous devez toorespond.</span><span class="sxs-lookup"><span data-stu-id="1d100-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="1d100-134">![Correction](./media/active-directory-identityprotection-flows/142.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="1d100-135">Récupération de connexion à risque</span><span class="sxs-lookup"><span data-stu-id="1d100-135">Risky sign-in recovery</span></span>
<span data-ttu-id="1d100-136">Lorsqu’un administrateur a configuré une stratégie de risques pour la connexion, les utilisateurs de hello affecté sont avertis quand ils essaient de toosign.</span><span class="sxs-lookup"><span data-stu-id="1d100-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="1d100-137">**flux de connexion présente des risques Hello comprend deux étapes :**</span><span class="sxs-lookup"><span data-stu-id="1d100-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="1d100-138">l’utilisateur Hello est informé que quelque chose d’inhabituel a été détecté sur leurs connectez-vous, telles que la connexion à partir d’un nouvel emplacement, appareil ou application.</span><span class="sxs-lookup"><span data-stu-id="1d100-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="1d100-139">![Correction](./media/active-directory-identityprotection-flows/120.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="1d100-140">utilisateur de Hello est requis tooprove leur identité en résolvant une vérification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="1d100-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="1d100-141">Si l’utilisateur de hello est inscrit pour l’authentification multifacteur dont ils ont besoin d’un numéro de téléphone de sécurité code tootheir de tooround-voyage.</span><span class="sxs-lookup"><span data-stu-id="1d100-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="1d100-142">Comme il s’agit seulement un risque de connexion et non un compte compromis, utilisateur de hello ne devra pas un mot de passe toochange hello dans ce flux.</span><span class="sxs-lookup"><span data-stu-id="1d100-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="1d100-143">![Correction](./media/active-directory-identityprotection-flows/121.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="1d100-144">Connexion à risque bloquée</span><span class="sxs-lookup"><span data-stu-id="1d100-144">Risky sign-in blocked</span></span>
<span data-ttu-id="1d100-145">Les administrateurs peuvent également choisir des tooset une ouverture de session risque stratégie tooblock des utilisateurs lors de l’authentification en fonction du niveau de risque hello.</span><span class="sxs-lookup"><span data-stu-id="1d100-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="1d100-146">tooget débloqué, les utilisateurs finaux doivent contacter un administrateur ou le support technique, ou ils peuvent essayez de vous connecter à partir d’un emplacement de votre choix ou un périphérique.</span><span class="sxs-lookup"><span data-stu-id="1d100-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="1d100-147">Il n’a pas la possibilité de récupérer lui-même son compte en résolvant l’authentification multifacteur dans ce cas précis.</span><span class="sxs-lookup"><span data-stu-id="1d100-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="1d100-148">![Correction](./media/active-directory-identityprotection-flows/200.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="1d100-149">Récupération de compte compromis</span><span class="sxs-lookup"><span data-stu-id="1d100-149">Compromised account recovery</span></span>
<span data-ttu-id="1d100-150">Lorsqu’une stratégie de sécurité risque utilisateur a été configurée, les utilisateurs qui répondent aux utilisateurs de hello risque au niveau spécifié dans la stratégie de hello (et sont donc supposés compromis) doivent passer par le flux de restauration hello utilisateur compromis avant qu’ils peuvent se connecter au.</span><span class="sxs-lookup"><span data-stu-id="1d100-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="1d100-151">**flux de restauration Hello utilisateur compromis comporte trois étapes :**</span><span class="sxs-lookup"><span data-stu-id="1d100-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="1d100-152">Hello l’utilisateur est informé que leur sécurité du compte est menacée en raison d’une activité suspecte ou une fuite des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1d100-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="1d100-153">![Correction](./media/active-directory-identityprotection-flows/101.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="1d100-154">utilisateur de Hello est requis tooprove leur identité en résolvant une vérification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="1d100-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="1d100-155">Si l’utilisateur de hello est inscrit pour l’authentification multifacteur ils peuvent récupérer automatiquement à partir de la compromission.</span><span class="sxs-lookup"><span data-stu-id="1d100-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="1d100-156">Ils devront tooround-trip un numéro de téléphone de sécurité code tootheir.</span><span class="sxs-lookup"><span data-stu-id="1d100-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="1d100-157">![Correction](./media/active-directory-identityprotection-flows/110.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="1d100-158">Enfin, hello utilisateur est forcé toochange leur mot de passe, car une autre personne peut avoir eu accès tootheir compte.</span><span class="sxs-lookup"><span data-stu-id="1d100-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="1d100-159">Vous trouverez ci-dessous des captures d’écran de cette expérience.</span><span class="sxs-lookup"><span data-stu-id="1d100-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="1d100-160">![Correction](./media/active-directory-identityprotection-flows/111.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="1d100-161">Compte compromis bloqué</span><span class="sxs-lookup"><span data-stu-id="1d100-161">Compromised account blocked</span></span>
<span data-ttu-id="1d100-162">tooget un utilisateur qui a été bloqué par une stratégie de sécurité utilisateur risque débloquée, utilisateur de hello doit contacter un administrateur ou le support technique.</span><span class="sxs-lookup"><span data-stu-id="1d100-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="1d100-163">Il n’a pas la possibilité de récupérer lui-même son compte en résolvant l’authentification multifacteur dans ce cas précis.</span><span class="sxs-lookup"><span data-stu-id="1d100-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="1d100-164">![Correction](./media/active-directory-identityprotection-flows/104.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="1d100-165">Réinitialiser le mot de passe</span><span class="sxs-lookup"><span data-stu-id="1d100-165">Reset password</span></span>
<span data-ttu-id="1d100-166">Si des utilisateurs compromis voient leur connexion bloquée, un administrateur peut générer un mot de passe temporaire pour eux.</span><span class="sxs-lookup"><span data-stu-id="1d100-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="1d100-167">les utilisateurs de Hello ont toochange leur mot de passe pendant une prochaine connexion de.</span><span class="sxs-lookup"><span data-stu-id="1d100-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="1d100-168">![Correction](./media/active-directory-identityprotection-flows/160.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="1d100-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="1d100-169">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1d100-169">See also</span></span>
* [<span data-ttu-id="1d100-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="1d100-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

