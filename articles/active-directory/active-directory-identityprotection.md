---
title: aaaAzure Active Directory Identity Protection | Documents Microsoft
description: "Découvrez comment Azure AD Identity Protection vous permet capacité hello toolimit une personne malveillante de tooexploit une identité compromise ou l’unité et toosecure une identité ou un périphérique qui a été précédemment toobe suspectée ou connu compromis."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="075b2-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="075b2-105">Azure Active Directory Identity Protection est une fonctionnalité d’édition hello Azure AD Premium P2 qui vous permet de :</span><span class="sxs-lookup"><span data-stu-id="075b2-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="075b2-106">Détecter les vulnérabilités potentielles qui affectent les identités de votre organisation</span><span class="sxs-lookup"><span data-stu-id="075b2-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="075b2-107">Configurer des actions suspectes de réponses automatiques toodetected qui sont les identités de l’organisation tooyour connexes</span><span class="sxs-lookup"><span data-stu-id="075b2-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="075b2-108">Examiner les incidents suspects et prendre les mesures appropriées tooresolve les</span><span class="sxs-lookup"><span data-stu-id="075b2-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="075b2-109">Prise en main</span><span class="sxs-lookup"><span data-stu-id="075b2-109">Getting started</span></span>

<span data-ttu-id="075b2-110">Microsoft sécurise les identités basées sur le cloud depuis plus de dix ans.</span><span class="sxs-lookup"><span data-stu-id="075b2-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="075b2-111">Avec la Protection d’identité Azure Active Directory, dans votre environnement, vous pouvez utiliser hello mêmes systèmes de protection Microsoft utilise des identités toosecure.</span><span class="sxs-lookup"><span data-stu-id="075b2-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="075b2-112">Hello grande majorité des prennent des failles de sécurité placer lorsque des personnes malveillantes accèdent environnement tooan d’accès par le vol d’identité d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="075b2-113">Années de hello, des personnes malveillantes sont devenues plus efficaces en tirant parti des violations de tiers et d’utilisation des attaques d’hameçonnage sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="075b2-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="075b2-114">Dès qu’une personne malveillante accès aux comptes d’utilisateur doté de privilèges faibles tooeven, il est relativement facile pour les ressources d’entreprise tooimportant toogain accès via un mouvement latéral.</span><span class="sxs-lookup"><span data-stu-id="075b2-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="075b2-115">Par conséquent, vous devez :</span><span class="sxs-lookup"><span data-stu-id="075b2-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="075b2-116">Protéger toutes les identités, quel que soit leur niveau de privilège</span><span class="sxs-lookup"><span data-stu-id="075b2-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="075b2-117">Empêcher proactivement le détournement des identités compromises</span><span class="sxs-lookup"><span data-stu-id="075b2-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="075b2-118">Détecter les identités compromises n’est pas chose aisée.</span><span class="sxs-lookup"><span data-stu-id="075b2-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="075b2-119">Azure Active Directory utilise des algorithmes d’apprentissage automatique adaptative et anomalies de toodetect heuristique et les incidents suspects qui indiquent potentiellement compromis des identités.</span><span class="sxs-lookup"><span data-stu-id="075b2-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="075b2-120">Protection de l’identité à l’aide de ces données, génère des rapports et les alertes qui permettent de vous hello de tooevaluate a détecté des problèmes et atténuation appropriés ou les actions de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="075b2-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="075b2-121">Mais Azure Active Directory Identity Protection est bien plus qu’un outil de surveillance et de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="075b2-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="075b2-122">tooprotect identités de votre organisation, vous pouvez configurer des stratégies basées sur les risques qui répondent automatiquement toodetected problèmes lorsqu’un niveau de risque spécifié a été atteint.</span><span class="sxs-lookup"><span data-stu-id="075b2-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="075b2-123">Ces stratégies, en outre tooother conditionnel accéder aux contrôles fournis par Azure Active Directory et EMS, pouvez bloquer automatiquement ou initier des actions de mise à jour ADAPTATIF, y compris les réinitialisations de mot de passe et la mise en œuvre l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="075b2-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="075b2-124">Fonctionnalités d’Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-124">Identity Protection capabilities</span></span>

<span data-ttu-id="075b2-125">**Détection des vulnérabilités et des comptes à risque :**</span><span class="sxs-lookup"><span data-stu-id="075b2-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="075b2-126">Fournir des recommandations personnalisées tooimprove globale posture de sécurité en mettant en surbrillance les vulnérabilités</span><span class="sxs-lookup"><span data-stu-id="075b2-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="075b2-127">Calcul des niveaux de risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="075b2-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="075b2-128">Calcul du niveau de risque des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="075b2-128">Calculating user risk levels</span></span>


<span data-ttu-id="075b2-129">**Examen des événements à risque :**</span><span class="sxs-lookup"><span data-stu-id="075b2-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="075b2-130">Envoi de notifications pour les événements à risque</span><span class="sxs-lookup"><span data-stu-id="075b2-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="075b2-131">Examen des événements à risque à l’aide d’informations contextuelles et pertinentes</span><span class="sxs-lookup"><span data-stu-id="075b2-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="075b2-132">En fournissant des workflows de base tootrack enquêtes</span><span class="sxs-lookup"><span data-stu-id="075b2-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="075b2-133">Fournissant un accès facile tooremediation des actions telles que la réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="075b2-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="075b2-134">**Stratégies d’accès conditionnel en fonction des risques :**</span><span class="sxs-lookup"><span data-stu-id="075b2-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="075b2-135">Stratégie toomitigate risquées connexions par le blocage des connexions ou exigeant l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="075b2-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="075b2-136">Stratégie tooblock ou des comptes d’utilisateur présente des risques sécurisé</span><span class="sxs-lookup"><span data-stu-id="075b2-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="075b2-137">Stratégie toorequire utilisateurs tooregister pour l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="075b2-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="075b2-138">Rôles de protection des identités (Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="075b2-138">Identity Protection roles</span></span>

<span data-ttu-id="075b2-139">activités de gestion hello tooload solde autour de votre implémentation de la Protection d’identité, vous pouvez attribuer plusieurs rôles.</span><span class="sxs-lookup"><span data-stu-id="075b2-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="075b2-140">Azure AD Identity Protection prend en charge 3 rôles d’annuaire :</span><span class="sxs-lookup"><span data-stu-id="075b2-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="075b2-141">Rôle</span><span class="sxs-lookup"><span data-stu-id="075b2-141">Role</span></span>                         | <span data-ttu-id="075b2-142">Peut</span><span class="sxs-lookup"><span data-stu-id="075b2-142">Can do</span></span>                          | <span data-ttu-id="075b2-143">Ne peut pas</span><span class="sxs-lookup"><span data-stu-id="075b2-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="075b2-144">Administrateur général</span><span class="sxs-lookup"><span data-stu-id="075b2-144">Global administrator</span></span>         | <span data-ttu-id="075b2-145">Accès complet tooIdentity Protection, intégrer Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="075b2-146">Administrateur de sécurité</span><span class="sxs-lookup"><span data-stu-id="075b2-146">Security administrator</span></span>       | <span data-ttu-id="075b2-147">Accès complet tooIdentity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="075b2-148">Onboard Identity Protection, réinitialiser les mots de passe pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="075b2-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="075b2-149">Lecteur de sécurité</span><span class="sxs-lookup"><span data-stu-id="075b2-149">Security reader</span></span>              | <span data-ttu-id="075b2-150">Accès seule tooIdentity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="075b2-151">Onboard Identity Protection, résoudre les utilisateurs, configurer les utilisateurs, réinitialiser les mots de passe</span><span class="sxs-lookup"><span data-stu-id="075b2-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="075b2-152">Pour plus d’informations, voir [Attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="075b2-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="075b2-153">Détection</span><span class="sxs-lookup"><span data-stu-id="075b2-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="075b2-154">Vulnérabilités</span><span class="sxs-lookup"><span data-stu-id="075b2-154">Vulnerabilities</span></span>

<span data-ttu-id="075b2-155">Azure Active Directory Identity Protection analyse votre configuration et détecte les vulnérabilités qui peuvent avoir un impact sur les identités de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="075b2-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="075b2-156">Pour en savoir plus, consultez [Vulnérabilités détectées par Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="075b2-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="075b2-157">Événements à risque</span><span class="sxs-lookup"><span data-stu-id="075b2-157">Risk events</span></span>

<span data-ttu-id="075b2-158">Azure Active Directory utilise des algorithmes et des paramètres heuristiques toodetect suspecte que les actions associées tooyour identités des utilisateurs d’apprentissage adaptatif.</span><span class="sxs-lookup"><span data-stu-id="075b2-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="075b2-159">système de Hello crée un enregistrement pour chaque action suspect détecté.</span><span class="sxs-lookup"><span data-stu-id="075b2-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="075b2-160">Ces enregistrements sont également appelés événements à risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="075b2-161">Pour en savoir plus, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="075b2-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="075b2-162">Investigation</span><span class="sxs-lookup"><span data-stu-id="075b2-162">Investigation</span></span>
<span data-ttu-id="075b2-163">Votre parcours via la Protection d’identité commence généralement par le tableau de bord hello Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="075b2-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="075b2-164">![Correction](./media/active-directory-identityprotection/1000.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="075b2-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="075b2-165">tableau de bord Hello vous donne accès à :</span><span class="sxs-lookup"><span data-stu-id="075b2-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="075b2-166">des rapports comme **Utilisateurs associés à un indicateur de risque**, **Événements à risque** et **Vulnérabilités** ;</span><span class="sxs-lookup"><span data-stu-id="075b2-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="075b2-167">Paramètres de configuration hello de votre **des stratégies de sécurité**, **Notifications** et **l’inscription de l’authentification multifacteur**</span><span class="sxs-lookup"><span data-stu-id="075b2-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="075b2-168">Il est généralement votre point de départ pour l’enquête, qui est le processus hello de révision des activités de hello, les journaux et autres informations pertinentes associée tooa risque de toodecide d’événements si les étapes de mise à jour ou d’atténuation sont nécessaires, et comment l’identité de hello a été compromis et comprendre comment hello compromis identité a été utilisée.</span><span class="sxs-lookup"><span data-stu-id="075b2-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="075b2-169">Vous pouvez lier votre toohello d’activités enquête [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection envoie par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="075b2-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="075b2-170">Hello sections suivantes vous fournissent plus de détails et les étapes hello tooan connexes enquête.</span><span class="sxs-lookup"><span data-stu-id="075b2-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="075b2-171">Connexions risquées</span><span class="sxs-lookup"><span data-stu-id="075b2-171">Risky sign-ins</span></span>

<span data-ttu-id="075b2-172">Azure Active Directory détecte les [types d’événements à risque](active-directory-reporting-risk-events.md#risk-event-types) en temps réel et hors connexion.</span><span class="sxs-lookup"><span data-stu-id="075b2-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="075b2-173">Chaque événement à risque qui a été détectée pour une connexion d’un utilisateur contribue tooa concept logique appelée connectez-vous présente des risques.</span><span class="sxs-lookup"><span data-stu-id="075b2-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="075b2-174">Une connexion à présente des risques est un indicateur pour une tentative de connexion qui a ne peut-être pas été exécutée par le propriétaire légitime de hello d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="075b2-175">Niveau de risque d’une connexion</span><span class="sxs-lookup"><span data-stu-id="075b2-175">Sign-in risk level</span></span>

<span data-ttu-id="075b2-176">Un niveau de risque de connexion est une indication (haute, moyenne ou faible) de probabilité de hello qu’une tentative de connexion n’a pas été effectuée par le propriétaire légitime de hello d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="075b2-177">Atténuation des événements à risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="075b2-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="075b2-178">Une limitation est une action toolimit hello capacité un appareil sans restauration de l’état sans échec tooa hello identité ou un périphérique ou un attaquant tooexploit une identité compromise.</span><span class="sxs-lookup"><span data-stu-id="075b2-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="075b2-179">Une atténuation ne résout pas les événements précédents connectez-vous risque associés hello identité ou d’appareil.</span><span class="sxs-lookup"><span data-stu-id="075b2-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="075b2-180">toomitigate risquée connexions automatiquement, vous pouvez configurer policicies de sécurité risque de connexion.</span><span class="sxs-lookup"><span data-stu-id="075b2-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="075b2-181">À l’aide de ces stratégies, considèrent le niveau de risque de hello d’utilisateur de hello ou hello connectez-vous tooblock connexions risquées ou exiger l’authentification multifacteur de hello utilisateur tooperform.</span><span class="sxs-lookup"><span data-stu-id="075b2-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="075b2-182">Ces actions peuvent empêcher un attaquant d’exploiter un endommagement de toocause d’identité et peuvent offrir une identité de hello toosecure heure.</span><span class="sxs-lookup"><span data-stu-id="075b2-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="075b2-183">Stratégie de sécurité en matière de risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="075b2-183">Sign-in risk security policy</span></span>
<span data-ttu-id="075b2-184">Une stratégie de connexion risque est une stratégie d’accès conditionnel qui prend la valeur hello risque tooa spécifique connectez-vous et applique les limitations de risques selon les règles et conditions prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="075b2-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="075b2-185">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1014.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="075b2-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="075b2-186">Azure AD Identity Protection vous permet de gérer l’atténuation hello de connexions présentant un risque en vous permettant de :</span><span class="sxs-lookup"><span data-stu-id="075b2-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="075b2-187">Définir hello utilisateurs et groupes hello une stratégie s’applique à :</span><span class="sxs-lookup"><span data-stu-id="075b2-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="075b2-188">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1015.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="075b2-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="075b2-189">Définissez hello connectez-vous risque seuil (faible, moyen ou élevé) qui déclenche la stratégie de hello :</span><span class="sxs-lookup"><span data-stu-id="075b2-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="075b2-190">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1016.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="075b2-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="075b2-191">Ensemble hello contrôles toobe appliquée au moment de la stratégie de hello déclenche :</span><span class="sxs-lookup"><span data-stu-id="075b2-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="075b2-192">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1017.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="075b2-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="075b2-193">Basculer hello de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="075b2-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="075b2-194">![Inscription à MFA](./media/active-directory-identityprotection/403.png "Inscription à MFA")</span><span class="sxs-lookup"><span data-stu-id="075b2-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="075b2-195">Passez en revue et évaluer l’impact de hello d’une modification avant son activation :</span><span class="sxs-lookup"><span data-stu-id="075b2-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="075b2-196">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1018.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="075b2-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="075b2-197">Vous devez tooknow</span><span class="sxs-lookup"><span data-stu-id="075b2-197">What you need tooknow</span></span>
<span data-ttu-id="075b2-198">Vous pouvez configurer une authentification multifacteur toorequire de stratégie de sécurité risque de connexion :</span><span class="sxs-lookup"><span data-stu-id="075b2-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="075b2-199">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1017.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="075b2-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="075b2-200">Toutefois, pour des raisons de sécurité, ce paramètre s’applique uniquement aux utilisateurs qui ont déjà été inscrits pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="075b2-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="075b2-201">Si l’authentification multifacteur de hello condition toorequire est respectée pour un utilisateur qui n’est pas encore inscrit pour l’authentification multifacteur, l’utilisateur de hello est bloquée.</span><span class="sxs-lookup"><span data-stu-id="075b2-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="075b2-202">Comme meilleure pratique, si vous souhaitez que l’authentification multifacteur de toorequire pour les connexions présentant un risque, vous devez :</span><span class="sxs-lookup"><span data-stu-id="075b2-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="075b2-203">Activer hello [stratégie d’inscription de l’authentification multifacteur](#multi-factor-authentication-registration-policy) pourquoi les utilisateurs affectés.</span><span class="sxs-lookup"><span data-stu-id="075b2-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="075b2-204">Nécessitent hello affectées toologin d’utilisateurs dans une session non risqué de tooperform une inscription de l’authentification Multifacteur</span><span class="sxs-lookup"><span data-stu-id="075b2-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="075b2-205">Suivre ces étapes permet de s’assurer que l’authentification multifacteur est requise pour une connexion à risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="075b2-206">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="075b2-206">Best practices</span></span>
<span data-ttu-id="075b2-207">Choix d’un **haute** seuil réduit le nombre de hello de fois où une stratégie est déclenchée et réduit hello impact toousers.</span><span class="sxs-lookup"><span data-stu-id="075b2-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="075b2-208">Toutefois, il exclut **faible** et **support** connexions signalées pour le risque d’une stratégie de hello, qui peut ne pas bloque un attaquant d’exploiter une identité compromise.</span><span class="sxs-lookup"><span data-stu-id="075b2-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="075b2-209">Lorsque le paramètre hello stratégie,</span><span class="sxs-lookup"><span data-stu-id="075b2-209">When setting hello policy,</span></span>

* <span data-ttu-id="075b2-210">Excluez les utilisateurs qui ne sont pas inscrits/ne peuvent pas s’inscrire à l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="075b2-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="075b2-211">Excluez les utilisateurs dans les paramètres régionaux où l’activation de la stratégie de hello n’est pas pratique (par exemple, aucun toohelpdesk accès)</span><span class="sxs-lookup"><span data-stu-id="075b2-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="075b2-212">Exclure les utilisateurs qui sont susceptibles de toogenerate un grand nombre de faux positifs (les développeurs et aux analystes en sécurité)</span><span class="sxs-lookup"><span data-stu-id="075b2-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="075b2-213">Utilisez un niveau de risque **Élevé** pendant le déploiement initial de la stratégie ou si vous devez minimiser la complexité pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="075b2-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="075b2-214">Utilisez un niveau de risque **Faible** si votre organisation nécessite une sécurité accrue.</span><span class="sxs-lookup"><span data-stu-id="075b2-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="075b2-215">La sélection d’un niveau de risque **Faible** complique la connexion pour les utilisateurs, mais renforce la sécurité.</span><span class="sxs-lookup"><span data-stu-id="075b2-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="075b2-216">Hello recommandé par défaut pour la plupart des organisations est tooconfigure une règle pour un **support** seuil toostrike un compromis entre facilité d’utilisation et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="075b2-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="075b2-217">stratégie de connexion risque Hello est :</span><span class="sxs-lookup"><span data-stu-id="075b2-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="075b2-218">Le trafic tooall appliqués et les connexions à l’aide de l’authentification moderne.</span><span class="sxs-lookup"><span data-stu-id="075b2-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="075b2-219">Tooapplications pas appliquées à l’aide des protocoles de sécurité plus anciens en désactivant le point de terminaison WS-Trust de hello à IDP hello fédéré, tel qu’AD FS.</span><span class="sxs-lookup"><span data-stu-id="075b2-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="075b2-220">Hello **événements à risque** page hello Identity Protection console répertorie tous les événements :</span><span class="sxs-lookup"><span data-stu-id="075b2-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="075b2-221">auxquels cette stratégie a été appliquée ;</span><span class="sxs-lookup"><span data-stu-id="075b2-221">This policy was applied to</span></span>
* <span data-ttu-id="075b2-222">Vous pouvez consulter l’activité hello et déterminer si action de hello a appropriées ou non</span><span class="sxs-lookup"><span data-stu-id="075b2-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="075b2-223">Pour une vue d’ensemble de hello liée à l’expérience utilisateur, consultez :</span><span class="sxs-lookup"><span data-stu-id="075b2-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="075b2-224">Récupération de connexion à risque</span><span class="sxs-lookup"><span data-stu-id="075b2-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="075b2-225">Connexion à risque bloquée</span><span class="sxs-lookup"><span data-stu-id="075b2-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="075b2-226">Expériences de connexion avec Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="075b2-227">**boîte de dialogue configuration associés tooopen hello**:</span><span class="sxs-lookup"><span data-stu-id="075b2-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="075b2-228">Sur hello **Azure AD Identity Protection** panneau, Bonjour **configurer** , cliquez sur **stratégie d’authentification risque**.</span><span class="sxs-lookup"><span data-stu-id="075b2-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="075b2-229">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1014.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="075b2-230">Utilisateurs associés à un indicateur de risque</span><span class="sxs-lookup"><span data-stu-id="075b2-230">Users flagged for risk</span></span>

<span data-ttu-id="075b2-231">Active tous les [risque d’événements](active-directory-identity-protection-risk-events.md) qui ont été détectés par Azure Active Directory pour un utilisateur contribuent tooa concept logique appelée risque de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="075b2-232">Un utilisateur signalé comme présentant un risque indique qu’un compte d’utilisateur est susceptible d’avoir été compromis.</span><span class="sxs-lookup"><span data-stu-id="075b2-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Utilisateurs associés à un indicateur de risque](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="075b2-234">Niveau de risque d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="075b2-234">User risk level</span></span>

<span data-ttu-id="075b2-235">Un niveau de risque d’utilisateur est une indication (haute, moyenne ou faible) de probabilité de hello que hello l’identité d’utilisateur a été compromise.</span><span class="sxs-lookup"><span data-stu-id="075b2-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="075b2-236">Il est calculé en fonction d’événements à risque hello utilisateur associés à l’identité d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="075b2-237">Hello état d’un événement à risque est **Active** ou **fermé**.</span><span class="sxs-lookup"><span data-stu-id="075b2-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="075b2-238">Uniquement les événements qui sont des risques **Active** contribuent le calcul du niveau de risque toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="075b2-239">niveau de risque utilisateur Hello est calculé à l’aide de hello suivant entrées :</span><span class="sxs-lookup"><span data-stu-id="075b2-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="075b2-240">Événements risque actif ayant un impact sur les utilisateurs hello</span><span class="sxs-lookup"><span data-stu-id="075b2-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="075b2-241">Niveau de risque de ces événements</span><span class="sxs-lookup"><span data-stu-id="075b2-241">Risk level of these events</span></span>
* <span data-ttu-id="075b2-242">Application ou non de mesures de correction</span><span class="sxs-lookup"><span data-stu-id="075b2-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="075b2-243">![Risques des utilisateurs](./media/active-directory-identityprotection/1031.png "Risques des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="075b2-244">Vous pouvez utiliser hello utilisateur risque niveaux toocreate stratégies d’accès conditionnel qui empêche les utilisateurs de risques de se connecter, ou forcer les toosecurely modifier leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="075b2-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="075b2-245">Fermeture manuelle des événements à risque</span><span class="sxs-lookup"><span data-stu-id="075b2-245">Closing risk events manually</span></span>

<span data-ttu-id="075b2-246">Dans la plupart des cas, vous prendra correctives telles que les événements de risque de fermer tooautomatically de réinitialisation de mot de passe sécurisé.</span><span class="sxs-lookup"><span data-stu-id="075b2-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="075b2-247">Toutefois, il se peut que cela ne soit pas toujours possible.</span><span class="sxs-lookup"><span data-stu-id="075b2-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="075b2-248">C’est par exemple, les cas de hello, lorsque :</span><span class="sxs-lookup"><span data-stu-id="075b2-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="075b2-249">un utilisateur avec des événements à risque actifs a été supprimé ;</span><span class="sxs-lookup"><span data-stu-id="075b2-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="075b2-250">Une enquête révèle qu’un événement à signalé risque a été effectuer par un utilisateur légitime de hello</span><span class="sxs-lookup"><span data-stu-id="075b2-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="075b2-251">Étant donné que les événements à risque qui sont **Active** calcul du toohello utilisateur risque de contribuer, vous avez peut-être toomanually réduire un niveau de risque en fermant les événements à risque manuellement.</span><span class="sxs-lookup"><span data-stu-id="075b2-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="075b2-252">Au cours de hello d’enquête, vous pouvez choisir tootake ces état de hello toochange actions d’un événement à risque des :</span><span class="sxs-lookup"><span data-stu-id="075b2-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="075b2-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="075b2-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="075b2-254">**Résoudre** - si après avoir examiné un événement à risque, vous avez une action de mise à jour appropriées en dehors de la Protection d’identité, et si vous pensez que l’événement hello risque doit être considérée comme fermée, l’événement de hello marque comme résolu.</span><span class="sxs-lookup"><span data-stu-id="075b2-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="075b2-255">Événements résolus définira tooClosed d’état de l’événement hello risque et événements risque de hello n’est plus contribuera toouser risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="075b2-256">**Marquer comme faux positif** : dans certains cas, il se peut qu’un événement à risque soit signalé à tort en tant que tel.</span><span class="sxs-lookup"><span data-stu-id="075b2-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="075b2-257">Pour réduire nombre hello de telles occurrences en marquant l’événement à risque hello comme faux positifs.</span><span class="sxs-lookup"><span data-stu-id="075b2-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="075b2-258">Cela permet de classification de hello tooimprove algorithmes d’événements similaires Bonjour future d’apprentissage hello.</span><span class="sxs-lookup"><span data-stu-id="075b2-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="075b2-259">état Hello d’événements de faux positifs est trop**fermé** et ils ne seront plus prises toouser risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="075b2-260">**Ignorer** : Si vous n’avez pas pris aucune action de mise à jour, mais hello risque événement toobe est supprimé de la liste active de hello, vous pouvez marquer un événement à risque ignorer et état de l’événement hello va être fermée.</span><span class="sxs-lookup"><span data-stu-id="075b2-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="075b2-261">Événements ignorés ne contribuent pas toouser risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="075b2-262">Cette option doit uniquement être utilisée dans des circonstances inhabituelles.</span><span class="sxs-lookup"><span data-stu-id="075b2-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="075b2-263">**Réactiver** -risque d’événements qui ont été fermées manuellement (en choisissant **résoudre**, **faux positif**, ou **ignorer**) peuvent être réactivés, paramètre hello statut de l’événement différé trop**Active**.</span><span class="sxs-lookup"><span data-stu-id="075b2-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="075b2-264">Événements à risque réactivé contribuent calcul du niveau de risque toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="075b2-265">Les événements à risque fermés à l’aide d’une mesure de correction (telle qu’une réinitialisation de mot de passe sécurisée) ne peuvent pas être réactivés.</span><span class="sxs-lookup"><span data-stu-id="075b2-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="075b2-266">**boîte de dialogue configuration associés tooopen hello**:</span><span class="sxs-lookup"><span data-stu-id="075b2-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="075b2-267">Sur hello **Azure AD Identity Protection** panneau, sous **examiner**, cliquez sur **risque d’événements**.</span><span class="sxs-lookup"><span data-stu-id="075b2-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="075b2-268">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1002.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="075b2-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="075b2-269">Bonjour **risque d’événements** , cliquez sur un risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="075b2-270">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1003.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="075b2-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="075b2-271">Dans Panneau de risques hello, cliquez sur un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="075b2-272">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1004.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="075b2-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="075b2-273">Fermeture manuelle de tous les événements à risque pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="075b2-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="075b2-274">Au lieu de fermeture manuellement individuellement d’événements à risque pour un utilisateur, Azure Active Directory Identity Protection vous donne également une méthode tooclose tous les événements pour un utilisateur avec un seul clic.</span><span class="sxs-lookup"><span data-stu-id="075b2-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="075b2-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="075b2-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="075b2-276">Lorsque vous cliquez sur **ignorer tous les événements**, tous les événements sont fermés et hello affectée utilisateur n’est plus exposés.</span><span class="sxs-lookup"><span data-stu-id="075b2-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="075b2-277">Correction des événements à risque d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="075b2-277">Remediating user risk events</span></span>

<span data-ttu-id="075b2-278">Une mise à jour est une toosecure action une identité ou un périphérique qui a été précédemment ou suspecté toobe compromis.</span><span class="sxs-lookup"><span data-stu-id="075b2-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="075b2-279">Une action de mise à jour restaure l’état sans échec tooa hello identité ou l’appareil et résout les événements précédents risque associés hello identité ou d’appareil.</span><span class="sxs-lookup"><span data-stu-id="075b2-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="075b2-280">événements à risque tooremediate utilisateur, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="075b2-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="075b2-281">Effectuer un mot de passe sécurisé tooremediate utilisateur risque les événements de réinitialisation manuelle</span><span class="sxs-lookup"><span data-stu-id="075b2-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="075b2-282">Configurer un toomitigate de stratégie de sécurité utilisateur risque ou de corriger automatiquement les événements à risque utilisateur</span><span class="sxs-lookup"><span data-stu-id="075b2-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="075b2-283">Une nouvelle image de périphérique de hello infecté</span><span class="sxs-lookup"><span data-stu-id="075b2-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="075b2-284">Réinitialisation manuelle et sécurisée du mot de passe</span><span class="sxs-lookup"><span data-stu-id="075b2-284">Manual secure password reset</span></span>
<span data-ttu-id="075b2-285">Une réinitialisation de mot de passe sécurisé est une mise à jour efficace pour de nombreux événements risque et lors de l’exécution, ferme ces événements à risque et automatiquement recalcule le niveau de risque hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="075b2-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="075b2-286">Vous pouvez utiliser hello Identity Protection du tableau de bord tooinitiate un mot de passe réinitialisé pour un utilisateur présentant un risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="075b2-287">boîte de dialogue associée Hello fournit deux méthodes différentes tooreset un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="075b2-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="075b2-288">**Réinitialisation du mot de passe** : sélectionnez **nécessitent hello utilisateur tooreset leur mot de passe** tooallow hello récupération tooself utilisateur si l’utilisateur de hello a inscrit pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="075b2-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="075b2-289">Lors de l’utilisateur hello suivant signe, utilisateur de hello sera requis toosolve stimulation avec succès d’une authentification multifacteur et mot de passe de hello toochange puis, forcé.</span><span class="sxs-lookup"><span data-stu-id="075b2-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="075b2-290">Cette option n’est pas disponible si le compte d’utilisateur hello n’est pas déjà inscrit de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="075b2-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="075b2-291">**Mot de passe temporaire** : sélectionnez **générer un mot de passe temporaire** tooimmediately invalider le mot de passe existant hello et créer un nouveau mot de passe temporaire pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="075b2-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="075b2-292">Envoyer hello nouveau mot de passe temporaire tooan autre adresse de messagerie pour l’utilisateur de hello ou un responsable de l’utilisateur toohello.</span><span class="sxs-lookup"><span data-stu-id="075b2-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="075b2-293">Parce que le mot de passe hello est temporaire, utilisateur de hello sera un mot de passe hello toochange demandées lors de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="075b2-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="075b2-294">![Stratégie](./media/active-directory-identityprotection/1005.png "Stratégie")</span><span class="sxs-lookup"><span data-stu-id="075b2-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="075b2-295">**boîte de dialogue configuration associés tooopen hello**:</span><span class="sxs-lookup"><span data-stu-id="075b2-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="075b2-296">Sur hello **Azure AD Identity Protection** panneau, cliquez sur **utilisateurs marqués pour risque**.</span><span class="sxs-lookup"><span data-stu-id="075b2-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="075b2-297">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1006.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="075b2-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="075b2-298">Dans la liste hello des utilisateurs, sélectionnez un utilisateur au moins un risque.</span><span class="sxs-lookup"><span data-stu-id="075b2-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="075b2-299">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1007.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="075b2-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="075b2-300">Dans le panneau d’utilisateur hello, cliquez sur **réinitialisation de mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="075b2-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="075b2-301">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1008.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="075b2-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="075b2-302">Stratégie de sécurité en matière de risque des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="075b2-302">User risk security policy</span></span>
<span data-ttu-id="075b2-303">Une stratégie de sécurité utilisateur risque est une stratégie d’accès conditionnel qui prend la valeur hello risque tooa au niveau utilisateur et applique les actions de mise à jour et d’atténuation selon les règles et conditions prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="075b2-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="075b2-304">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1009.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="075b2-305">Azure AD Identity Protection vous permet de gérer l’atténuation de hello et mise à jour des utilisateurs marquées pour risque par ce qui vous permet :</span><span class="sxs-lookup"><span data-stu-id="075b2-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="075b2-306">Définir hello utilisateurs et groupes hello une stratégie s’applique à :</span><span class="sxs-lookup"><span data-stu-id="075b2-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="075b2-307">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1010.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="075b2-308">Définissez hello utilisateur risque seuil (faible, moyen ou élevé) qui déclenche la stratégie de hello :</span><span class="sxs-lookup"><span data-stu-id="075b2-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="075b2-309">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1011.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="075b2-310">Ensemble hello contrôles toobe appliquée au moment de la stratégie de hello déclenche :</span><span class="sxs-lookup"><span data-stu-id="075b2-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="075b2-311">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1012.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="075b2-312">Basculer hello de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="075b2-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="075b2-313">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/403.png "Inscription à MFA")</span><span class="sxs-lookup"><span data-stu-id="075b2-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="075b2-314">Passez en revue et évaluer l’impact de hello d’une modification avant son activation :</span><span class="sxs-lookup"><span data-stu-id="075b2-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="075b2-315">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1013.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="075b2-316">Choix d’un **haute** seuil réduit le nombre de hello de fois où une stratégie est déclenchée et réduit hello impact toousers.</span><span class="sxs-lookup"><span data-stu-id="075b2-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="075b2-317">Toutefois, il exclut **faible** et **support** utilisateurs signalées pour le risque d’une stratégie de hello, qui ne peut pas sécuriser les identités ou les appareils qui ont été précédemment ou suspectées toobe compromis.</span><span class="sxs-lookup"><span data-stu-id="075b2-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="075b2-318">Lorsque le paramètre hello stratégie,</span><span class="sxs-lookup"><span data-stu-id="075b2-318">When setting hello policy,</span></span>

* <span data-ttu-id="075b2-319">Exclure les utilisateurs qui sont susceptibles de toogenerate un grand nombre de faux positifs (les développeurs et aux analystes en sécurité)</span><span class="sxs-lookup"><span data-stu-id="075b2-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="075b2-320">Excluez les utilisateurs dans les paramètres régionaux où l’activation de la stratégie de hello n’est pas pratique (par exemple, aucun toohelpdesk accès)</span><span class="sxs-lookup"><span data-stu-id="075b2-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="075b2-321">Utilisez un niveau de risque **Élevé** pendant le déploiement initial de la stratégie ou si vous devez minimiser la complexité pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="075b2-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="075b2-322">Utilisez un niveau de risque **Faible** si votre organisation nécessite une sécurité accrue.</span><span class="sxs-lookup"><span data-stu-id="075b2-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="075b2-323">La sélection d’un niveau de risque **Faible** complique la connexion pour les utilisateurs, mais renforce la sécurité.</span><span class="sxs-lookup"><span data-stu-id="075b2-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="075b2-324">Hello recommandé par défaut pour la plupart des organisations est tooconfigure une règle pour un **support** seuil toostrike un compromis entre facilité d’utilisation et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="075b2-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="075b2-325">Pour une vue d’ensemble de hello liée à l’expérience utilisateur, consultez :</span><span class="sxs-lookup"><span data-stu-id="075b2-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="075b2-326">[Flux de récupération de compte compromis](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="075b2-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="075b2-327">[Flux de compte compromis bloqué](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="075b2-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="075b2-328">**boîte de dialogue configuration associés tooopen hello**:</span><span class="sxs-lookup"><span data-stu-id="075b2-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="075b2-329">Sur hello **Azure AD Identity Protection** panneau, Bonjour **configurer** , cliquez sur **stratégie des risques utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="075b2-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="075b2-330">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1009.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="075b2-331">Atténuation des événements à risque d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="075b2-331">Mitigating user risk events</span></span>
<span data-ttu-id="075b2-332">Les administrateurs peuvent définir un utilisateur risque sécurité stratégie tooblock utilisateurs lors de l’authentification en fonction du niveau de risque hello.</span><span class="sxs-lookup"><span data-stu-id="075b2-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="075b2-333">Le blocage d’une connexion :</span><span class="sxs-lookup"><span data-stu-id="075b2-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="075b2-334">Empêche la génération de nouveaux événements de risque d’utilisateur pour l’utilisateur de hello affectée hello</span><span class="sxs-lookup"><span data-stu-id="075b2-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="075b2-335">Permet aux administrateurs toomanually corriger les événements à risque hello affectant l’identité de l’utilisateur hello et restaurez-la état sécurisé de tooa</span><span class="sxs-lookup"><span data-stu-id="075b2-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="075b2-336">Stratégie d’inscription à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="075b2-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="075b2-337">L’authentification multifacteur Azure est une méthode de vérification qui vous sont qui nécessite l’utilisation de hello de plus qu’un nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="075b2-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="075b2-338">Il fournit une deuxième couche de sécurité toouser connexions et transactions.</span><span class="sxs-lookup"><span data-stu-id="075b2-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="075b2-339">Nous vous recommandons d’exiger l’authentification multifacteur d’Azure des connexions des utilisateurs pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="075b2-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="075b2-340">Elle fournit une authentification renforcée avec un éventail d’options de vérification simples.</span><span class="sxs-lookup"><span data-stu-id="075b2-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="075b2-341">Joue un rôle clé dans la préparation de votre organisation tooprotect et récupérer à partir de compromission du compte</span><span class="sxs-lookup"><span data-stu-id="075b2-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="075b2-342">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1019.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="075b2-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="075b2-343">Pour plus d’informations, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="075b2-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="075b2-344">Azure AD Identity Protection vous permet de gérer la sortie hello d’enregistrement de l’authentification multifacteur en configurant une stratégie qui vous permet de :</span><span class="sxs-lookup"><span data-stu-id="075b2-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="075b2-345">Définir hello utilisateurs et groupes hello une stratégie s’applique à :</span><span class="sxs-lookup"><span data-stu-id="075b2-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="075b2-346">![Stratégie MFA](./media/active-directory-identityprotection/1020.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="075b2-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="075b2-347">Ensemble hello contrôles toobe appliquée au moment de la stratégie de hello déclenche ::</span><span class="sxs-lookup"><span data-stu-id="075b2-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="075b2-348">![Stratégie MFA](./media/active-directory-identityprotection/1021.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="075b2-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="075b2-349">Basculer hello de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="075b2-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="075b2-350">![Stratégie MFA](./media/active-directory-identityprotection/403.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="075b2-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="075b2-351">Afficher l’état de l’enregistrement actuel hello :</span><span class="sxs-lookup"><span data-stu-id="075b2-351">View hello current registration status:</span></span>

    <span data-ttu-id="075b2-352">![Stratégie MFA](./media/active-directory-identityprotection/1022.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="075b2-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="075b2-353">Pour une vue d’ensemble de hello liée à l’expérience utilisateur, consultez :</span><span class="sxs-lookup"><span data-stu-id="075b2-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="075b2-354">[Processus d’inscription à l’authentification multifacteur](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="075b2-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="075b2-355">[Expériences de connexion avec Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="075b2-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="075b2-356">**boîte de dialogue configuration associés tooopen hello**:</span><span class="sxs-lookup"><span data-stu-id="075b2-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="075b2-357">Sur hello **Azure AD Identity Protection** panneau, Bonjour **configurer** , cliquez sur **l’enregistrement de l’authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="075b2-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="075b2-358">![Stratégie MFA](./media/active-directory-identityprotection/1019.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="075b2-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="075b2-359">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="075b2-359">Next steps</span></span>
* [<span data-ttu-id="075b2-360">Channel 9 : Azure AD and Identity Show: Identity Protection Preview (Émission sur Azure AD et l’identité : présentation d’Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="075b2-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="075b2-361">Activer Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="075b2-362">Vulnérabilités détectées par Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="075b2-363">Événements à risque dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="075b2-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="075b2-364">Notifications d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="075b2-365">Manuel d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="075b2-366">Glossaire d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="075b2-367">Expériences de connexion avec Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="075b2-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="075b2-368">Azure Active Directory Identity Protection - comment toounblock utilisateurs</span><span class="sxs-lookup"><span data-stu-id="075b2-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="075b2-369">Prise en main d’Azure Active Directory Identity Protection et de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="075b2-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
