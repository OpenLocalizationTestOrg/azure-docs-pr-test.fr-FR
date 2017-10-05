---
title: "Expériences de connexion avec Azure AD Identity Protection | Microsoft Docs"
description: "Fournit une vue d’ensemble de l’expérience utilisateur lorsque Identity Protection a atténué ou corrigé la connexion d’un utilisateur ou lorsque l’authentification multifacteur est requise par une stratégie."
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
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="0f363-104">Expériences de connexion avec Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="0f363-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="0f363-105">Avec Azure Active Directory Identity Protection, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="0f363-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="0f363-106">exiger que les utilisateurs s’inscrivent à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="0f363-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="0f363-107">gérer les connexions risquées et les utilisateurs compromis</span><span class="sxs-lookup"><span data-stu-id="0f363-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="0f363-108">La réponse du système à ces problèmes a un impact sur l’expérience de connexion d’un utilisateur, car la connexion à l’aide d’un nom d’utilisateur et d’un mot de passe seulement ne sera plus possible.</span><span class="sxs-lookup"><span data-stu-id="0f363-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="0f363-109">Des étapes supplémentaires sont nécessaires pour rétablir l’accès d’un utilisateur en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f363-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="0f363-110">Cette rubrique donne une vue d’ensemble de l’expérience de connexion d’un utilisateur pour tous les cas qui peuvent se produire.</span><span class="sxs-lookup"><span data-stu-id="0f363-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="0f363-111">**Authentification multifacteur**</span><span class="sxs-lookup"><span data-stu-id="0f363-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="0f363-112">Inscription à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="0f363-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="0f363-113">**Connexion risquée**</span><span class="sxs-lookup"><span data-stu-id="0f363-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="0f363-114">Récupération de connexion à risque</span><span class="sxs-lookup"><span data-stu-id="0f363-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="0f363-115">Connexion à risque bloquée</span><span class="sxs-lookup"><span data-stu-id="0f363-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="0f363-116">Inscription à l’authentification multifacteur au cours d’une connexion à risque</span><span class="sxs-lookup"><span data-stu-id="0f363-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="0f363-117">**Utilisateur à risque**</span><span class="sxs-lookup"><span data-stu-id="0f363-117">**User at risk**</span></span>

* <span data-ttu-id="0f363-118">Récupération de compte compromis</span><span class="sxs-lookup"><span data-stu-id="0f363-118">Compromised account recovery</span></span>
* <span data-ttu-id="0f363-119">Compte compromis bloqué</span><span class="sxs-lookup"><span data-stu-id="0f363-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="0f363-120">Inscription à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="0f363-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="0f363-121">L’utilisateur bénéficie d’une expérience optimale pour le flux de récupération de compte compromis et de connexion à risque lorsqu’il peut effectuer lui-même l’opération de récupération.</span><span class="sxs-lookup"><span data-stu-id="0f363-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="0f363-122">Si des utilisateurs sont inscrits à l’authentification multifacteur, ils ont déjà un numéro de téléphone associé à leur compte qu’ils peuvent utiliser pour répondre aux questions de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f363-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="0f363-123">La récupération d’un compte suite à sa compromission ne nécessite pas l’intervention du support technique ou d’un administrateur.</span><span class="sxs-lookup"><span data-stu-id="0f363-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="0f363-124">Par conséquent, nous vous recommandons vivement de demander à vos utilisateurs de s’inscrire à l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="0f363-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="0f363-125">Les administrateurs peuvent :</span><span class="sxs-lookup"><span data-stu-id="0f363-125">Administrators can:</span></span>

* <span data-ttu-id="0f363-126">définir une stratégie qui impose aux utilisateurs d’ajouter une vérification de sécurité supplémentaire à leur compte ;</span><span class="sxs-lookup"><span data-stu-id="0f363-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="0f363-127">autoriser les utilisateurs à ignorer l’inscription à l’authentification multifacteur pendant 30 jours maximum, s’ils souhaitent leur accorder un délai de grâce avant l’inscription.</span><span class="sxs-lookup"><span data-stu-id="0f363-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="0f363-128">**L’inscription à l’authentification multifacteur comporte trois étapes :**</span><span class="sxs-lookup"><span data-stu-id="0f363-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="0f363-129">Dans la première étape, l’utilisateur reçoit une notification concernant la nécessité d’inscrire le compte à l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="0f363-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="0f363-130">![Correction](./media/active-directory-identityprotection-flows/140.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="0f363-131">Pour configurer l’authentification multifacteur, vous devez indiquer au système comment vous souhaitez être contacté.</span><span class="sxs-lookup"><span data-stu-id="0f363-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="0f363-132">![Correction](./media/active-directory-identityprotection-flows/141.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="0f363-133">Le système vous envoie un défi et vous devez y répondre.</span><span class="sxs-lookup"><span data-stu-id="0f363-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="0f363-134">![Correction](./media/active-directory-identityprotection-flows/142.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="0f363-135">Récupération de connexion à risque</span><span class="sxs-lookup"><span data-stu-id="0f363-135">Risky sign-in recovery</span></span>
<span data-ttu-id="0f363-136">Lorsqu’un administrateur a configuré une stratégie pour les risques à la connexion, les utilisateurs affectés sont avertis quand ils tentent de se connecter.</span><span class="sxs-lookup"><span data-stu-id="0f363-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="0f363-137">**Le flux de connexion à risque comporte deux étapes :**</span><span class="sxs-lookup"><span data-stu-id="0f363-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="0f363-138">L’utilisateur est informé que quelque chose d’inhabituel a été détecté concernant sa connexion, par exemple en cas de connexion depuis un nouvel emplacement, un nouvel appareil ou une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="0f363-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="0f363-139">![Correction](./media/active-directory-identityprotection-flows/120.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="0f363-140">L’utilisateur doit prouver son identité en répondant à une question de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f363-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="0f363-141">Si l’utilisateur est inscrit à l’authentification multifacteur, il doit saisir un code de sécurité envoyé sur son téléphone.</span><span class="sxs-lookup"><span data-stu-id="0f363-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="0f363-142">Comme il s’agit simplement d’une connexion à risque et non pas d’un compte compromis, l’utilisateur ne doit pas changer le mot de passe dans ce flux.</span><span class="sxs-lookup"><span data-stu-id="0f363-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="0f363-143">![Correction](./media/active-directory-identityprotection-flows/121.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="0f363-144">Connexion à risque bloquée</span><span class="sxs-lookup"><span data-stu-id="0f363-144">Risky sign-in blocked</span></span>
<span data-ttu-id="0f363-145">Les administrateurs peuvent également choisir de définir une stratégie en matière de risque à la connexion pour bloquer les utilisateurs lors de la connexion selon le niveau de risque.</span><span class="sxs-lookup"><span data-stu-id="0f363-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="0f363-146">Pour débloquer leur accès, les utilisateurs finaux doivent contacter un administrateur ou leur support technique, ou ils peuvent essayer de se connecter depuis un emplacement ou un appareil connu.</span><span class="sxs-lookup"><span data-stu-id="0f363-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="0f363-147">Il n’a pas la possibilité de récupérer lui-même son compte en résolvant l’authentification multifacteur dans ce cas précis.</span><span class="sxs-lookup"><span data-stu-id="0f363-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="0f363-148">![Correction](./media/active-directory-identityprotection-flows/200.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="0f363-149">Récupération de compte compromis</span><span class="sxs-lookup"><span data-stu-id="0f363-149">Compromised account recovery</span></span>
<span data-ttu-id="0f363-150">Lorsqu’une stratégie de sécurité en matière de risque des utilisateurs a été configurée, les utilisateurs dont le niveau de risque correspond à celui spécifié dans la stratégie (et qui sont donc considérés comme compromis) doivent passer par le flux de récupération de compte compromis avant de pouvoir se connecter.</span><span class="sxs-lookup"><span data-stu-id="0f363-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="0f363-151">**Le flux de récupération de compte compromis comporte trois étapes :**</span><span class="sxs-lookup"><span data-stu-id="0f363-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="0f363-152">L’utilisateur est informé que la sécurité de son compte est menacée en raison d’activités suspectes ou de la divulgation de ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0f363-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="0f363-153">![Correction](./media/active-directory-identityprotection-flows/101.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="0f363-154">L’utilisateur doit prouver son identité en répondant à une question de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f363-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="0f363-155">Si l’utilisateur est inscrit à l’authentification multifacteur, il peut récupérer lui-même son compte compromis.</span><span class="sxs-lookup"><span data-stu-id="0f363-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="0f363-156">Il devra saisir un code de sécurité envoyé sur son téléphone.</span><span class="sxs-lookup"><span data-stu-id="0f363-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="0f363-157">![Correction](./media/active-directory-identityprotection-flows/110.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="0f363-158">Enfin, l’utilisateur est obligé de changer son mot de passe, car il se peut que quelqu’un d’autre ait eu accès à son compte.</span><span class="sxs-lookup"><span data-stu-id="0f363-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="0f363-159">Vous trouverez ci-dessous des captures d’écran de cette expérience.</span><span class="sxs-lookup"><span data-stu-id="0f363-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="0f363-160">![Correction](./media/active-directory-identityprotection-flows/111.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="0f363-161">Compte compromis bloqué</span><span class="sxs-lookup"><span data-stu-id="0f363-161">Compromised account blocked</span></span>
<span data-ttu-id="0f363-162">Pour débloquer un compte bloqué par une stratégie de sécurité en matière de risque des utilisateurs, l’utilisateur doit contacter un administrateur ou son support technique.</span><span class="sxs-lookup"><span data-stu-id="0f363-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="0f363-163">Il n’a pas la possibilité de récupérer lui-même son compte en résolvant l’authentification multifacteur dans ce cas précis.</span><span class="sxs-lookup"><span data-stu-id="0f363-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="0f363-164">![Correction](./media/active-directory-identityprotection-flows/104.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="0f363-165">Réinitialiser le mot de passe</span><span class="sxs-lookup"><span data-stu-id="0f363-165">Reset password</span></span>
<span data-ttu-id="0f363-166">Si des utilisateurs compromis voient leur connexion bloquée, un administrateur peut générer un mot de passe temporaire pour eux.</span><span class="sxs-lookup"><span data-stu-id="0f363-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="0f363-167">Les utilisateurs devront changer leur mot de passe la prochaine fois qu’ils se connecteront.</span><span class="sxs-lookup"><span data-stu-id="0f363-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="0f363-168">![Correction](./media/active-directory-identityprotection-flows/160.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="0f363-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="0f363-169">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0f363-169">See also</span></span>
* [<span data-ttu-id="0f363-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="0f363-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

