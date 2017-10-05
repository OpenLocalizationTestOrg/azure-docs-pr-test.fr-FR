---
title: "Azure Active Directory Identity Protection | Microsoft Docs"
description: "Découvrez comment Azure AD Identity Protection vous permet de limiter la capacité d’un cybercriminel à exploiter une identité ou un appareil compromis et de sécuriser une identité ou un appareil déjà identifié comme potentiellement ou effectivement compromis."
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
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="f91be-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="f91be-105">Azure Active Directory Identity Protection est une fonctionnalité de l’édition Azure AD Premium P2 qui vous permet de :</span><span class="sxs-lookup"><span data-stu-id="f91be-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="f91be-106">Détecter les vulnérabilités potentielles qui affectent les identités de votre organisation</span><span class="sxs-lookup"><span data-stu-id="f91be-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="f91be-107">Configurer des réponses automatiques aux actions suspectes détectées qui sont liées aux identités de votre organisation</span><span class="sxs-lookup"><span data-stu-id="f91be-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="f91be-108">Examiner les incidents suspects et prendre les mesures appropriées pour les résoudre</span><span class="sxs-lookup"><span data-stu-id="f91be-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="f91be-109">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f91be-109">Getting started</span></span>

<span data-ttu-id="f91be-110">Microsoft sécurise les identités basées sur le cloud depuis plus de dix ans.</span><span class="sxs-lookup"><span data-stu-id="f91be-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="f91be-111">Avec Azure Active Directory Identity Protection, vous pouvez dans votre environnement utiliser les mêmes systèmes de protection que Microsoft pour sécuriser les identités.</span><span class="sxs-lookup"><span data-stu-id="f91be-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="f91be-112">La grande majorité des violations de sécurité ont lieu lorsque des cybercriminels parviennent à accéder à un environnement en volant l’identité d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="f91be-113">Aujourd’hui, les cybercriminels arrivent de plus en plus à exploiter les failles de fournisseurs tiers et utilisent des attaques par hameçonnage (ou « phishing ») sophistiquées toujours plus efficaces.</span><span class="sxs-lookup"><span data-stu-id="f91be-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="f91be-114">Dès qu’un cybercriminel accède à un compte d’utilisateur, même si les privilèges de celui-ci sont faibles, il peut facilement accéder à des ressources importantes pour l’entreprise de manière latérale.</span><span class="sxs-lookup"><span data-stu-id="f91be-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="f91be-115">Par conséquent, vous devez :</span><span class="sxs-lookup"><span data-stu-id="f91be-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="f91be-116">Protéger toutes les identités, quel que soit leur niveau de privilège</span><span class="sxs-lookup"><span data-stu-id="f91be-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="f91be-117">Empêcher proactivement le détournement des identités compromises</span><span class="sxs-lookup"><span data-stu-id="f91be-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="f91be-118">Détecter les identités compromises n’est pas chose aisée.</span><span class="sxs-lookup"><span data-stu-id="f91be-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="f91be-119">Azure Active Directory utilise des algorithmes de Machine Learning et des modèles heuristiques adaptatifs pour détecter les anomalies et les incidents suspects qui révèlent des identités potentiellement compromises.</span><span class="sxs-lookup"><span data-stu-id="f91be-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="f91be-120">Grâce à ces données, Identity Protection génère des rapports et des alertes qui vous permettent d’évaluer les problèmes détectés et de prendre les mesures de correction ou d’atténuation qui s’imposent.</span><span class="sxs-lookup"><span data-stu-id="f91be-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="f91be-121">Mais Azure Active Directory Identity Protection est bien plus qu’un outil de surveillance et de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="f91be-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="f91be-122">Pour protéger les identités de votre organisation, vous pouvez configurer des stratégies qui répondent automatiquement aux problèmes détectés lorsqu’un niveau de risque spécifié est atteint.</span><span class="sxs-lookup"><span data-stu-id="f91be-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="f91be-123">Outre les autres contrôles d’accès conditionnel fournis par Azure Active Directory et EMS, ces stratégies peuvent automatiquement bloquer ou déclencher des mesures de correction adaptatives qui incluent des réinitialisations de mot de passe et la mise en œuvre de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="f91be-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="f91be-124">Fonctionnalités d’Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-124">Identity Protection capabilities</span></span>

<span data-ttu-id="f91be-125">**Détection des vulnérabilités et des comptes à risque :**</span><span class="sxs-lookup"><span data-stu-id="f91be-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="f91be-126">Recommandations personnalisées visant à améliorer la posture de sécurité globale en mettant en évidence les vulnérabilités</span><span class="sxs-lookup"><span data-stu-id="f91be-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="f91be-127">Calcul des niveaux de risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="f91be-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="f91be-128">Calcul du niveau de risque des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f91be-128">Calculating user risk levels</span></span>


<span data-ttu-id="f91be-129">**Examen des événements à risque :**</span><span class="sxs-lookup"><span data-stu-id="f91be-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="f91be-130">Envoi de notifications pour les événements à risque</span><span class="sxs-lookup"><span data-stu-id="f91be-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="f91be-131">Examen des événements à risque à l’aide d’informations contextuelles et pertinentes</span><span class="sxs-lookup"><span data-stu-id="f91be-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="f91be-132">Workflows de base pour le suivi des investigations</span><span class="sxs-lookup"><span data-stu-id="f91be-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="f91be-133">Accès rapide à des mesures de correction telles que la réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="f91be-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="f91be-134">**Stratégies d’accès conditionnel en fonction des risques :**</span><span class="sxs-lookup"><span data-stu-id="f91be-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="f91be-135">Stratégie pour atténuer les connexions à risque en bloquant les connexions ou en imposant des demandes d’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="f91be-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="f91be-136">Stratégie pour bloquer ou sécuriser les comptes d’utilisateurs à risque</span><span class="sxs-lookup"><span data-stu-id="f91be-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="f91be-137">Stratégie pour exiger que les utilisateurs s’inscrivent à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="f91be-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="f91be-138">Rôles de protection des identités (Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="f91be-138">Identity Protection roles</span></span>

<span data-ttu-id="f91be-139">Pour équilibrer la charge des activités de gestion en ce qui concerne votre implémentation de la protection des identités, vous pouvez attribuer plusieurs rôles.</span><span class="sxs-lookup"><span data-stu-id="f91be-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="f91be-140">Azure AD Identity Protection prend en charge 3 rôles d’annuaire :</span><span class="sxs-lookup"><span data-stu-id="f91be-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="f91be-141">Rôle</span><span class="sxs-lookup"><span data-stu-id="f91be-141">Role</span></span>                         | <span data-ttu-id="f91be-142">Peut</span><span class="sxs-lookup"><span data-stu-id="f91be-142">Can do</span></span>                          | <span data-ttu-id="f91be-143">Ne peut pas</span><span class="sxs-lookup"><span data-stu-id="f91be-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="f91be-144">Administrateur général</span><span class="sxs-lookup"><span data-stu-id="f91be-144">Global administrator</span></span>         | <span data-ttu-id="f91be-145">Accès complet à Identity Protection, Onboard Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="f91be-146">Administrateur de sécurité</span><span class="sxs-lookup"><span data-stu-id="f91be-146">Security administrator</span></span>       | <span data-ttu-id="f91be-147">Accès complet à Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-147">Full access to Identity Protection</span></span> | <span data-ttu-id="f91be-148">Onboard Identity Protection, réinitialiser les mots de passe pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91be-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="f91be-149">Lecteur de sécurité</span><span class="sxs-lookup"><span data-stu-id="f91be-149">Security reader</span></span>              | <span data-ttu-id="f91be-150">Accès en lecture seule à Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="f91be-151">Onboard Identity Protection, résoudre les utilisateurs, configurer les utilisateurs, réinitialiser les mots de passe</span><span class="sxs-lookup"><span data-stu-id="f91be-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="f91be-152">Pour plus d’informations, voir [Attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f91be-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="f91be-153">Détection</span><span class="sxs-lookup"><span data-stu-id="f91be-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="f91be-154">Vulnérabilités</span><span class="sxs-lookup"><span data-stu-id="f91be-154">Vulnerabilities</span></span>

<span data-ttu-id="f91be-155">Azure Active Directory Identity Protection analyse votre configuration et détecte les vulnérabilités qui peuvent avoir un impact sur les identités de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f91be-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="f91be-156">Pour en savoir plus, consultez [Vulnérabilités détectées par Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="f91be-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="f91be-157">Événements à risque</span><span class="sxs-lookup"><span data-stu-id="f91be-157">Risk events</span></span>

<span data-ttu-id="f91be-158">Azure Active Directory utilise les algorithmes de Machine Learning et des modèles heuristiques adaptatifs pour détecter les actions suspectes liées aux identités de votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="f91be-159">Le système crée un enregistrement pour chaque action suspecte détectée.</span><span class="sxs-lookup"><span data-stu-id="f91be-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="f91be-160">Ces enregistrements sont également appelés événements à risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="f91be-161">Pour en savoir plus, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="f91be-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="f91be-162">Investigation</span><span class="sxs-lookup"><span data-stu-id="f91be-162">Investigation</span></span>
<span data-ttu-id="f91be-163">Votre parcours dans Identity Protection commence généralement par le tableau de bord d’Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="f91be-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="f91be-164">![Correction](./media/active-directory-identityprotection/1000.png "Correction")</span><span class="sxs-lookup"><span data-stu-id="f91be-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="f91be-165">Le tableau de bord vous donne accès à :</span><span class="sxs-lookup"><span data-stu-id="f91be-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="f91be-166">des rapports comme **Utilisateurs associés à un indicateur de risque**, **Événements à risque** et **Vulnérabilités** ;</span><span class="sxs-lookup"><span data-stu-id="f91be-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="f91be-167">des paramètres vous permettant notamment de configurer vos **stratégies de sécurité**, vos **notifications** et **l’inscription à l’authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="f91be-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="f91be-168">Il s’agit généralement de votre point de départ pour l’investigation, le processus consistant à vérifier les activités, les journaux et les autres informations pertinentes concernant un événement à risque, afin de déterminer s’il est nécessaire d’appliquer des mesures de correction ou d’atténuation, de comprendre comment l’identité a été compromise et d’identifier la manière dont l’identité compromise a été exploitée.</span><span class="sxs-lookup"><span data-stu-id="f91be-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="f91be-169">Vous pouvez lier vos activités d’investigation aux [notifications](active-directory-identityprotection-notifications.md) d’Azure Active Directory Protection envoyées par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="f91be-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="f91be-170">Les sections suivantes fournissent plus de détails, ainsi que les étapes liées à une investigation.</span><span class="sxs-lookup"><span data-stu-id="f91be-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="f91be-171">Connexions risquées</span><span class="sxs-lookup"><span data-stu-id="f91be-171">Risky sign-ins</span></span>

<span data-ttu-id="f91be-172">Azure Active Directory détecte les [types d’événements à risque](active-directory-reporting-risk-events.md#risk-event-types) en temps réel et hors connexion.</span><span class="sxs-lookup"><span data-stu-id="f91be-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="f91be-173">Tous les événements à risque qui sont détectés pendant la connexion d’un utilisateur viennent alimenter un concept logique appelé « connexion risquée ».</span><span class="sxs-lookup"><span data-stu-id="f91be-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="f91be-174">Une connexion risquée est une tentative de connexion susceptible d’émaner d’un utilisateur autre que le propriétaire légitime d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="f91be-175">Niveau de risque d’une connexion</span><span class="sxs-lookup"><span data-stu-id="f91be-175">Sign-in risk level</span></span>

<span data-ttu-id="f91be-176">Un niveau de risque de connexion est une indication de la probabilité (haute, moyenne ou faible) qu’une tentative de connexion n’émane pas du propriétaire légitime d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="f91be-177">Atténuation des événements à risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="f91be-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="f91be-178">Une atténuation est une mesure visant à limiter la probabilité qu’un pirate exploite une identité ou un appareil compromis, mais qui ne permet pas de rétablir la sécurité de l’identité ou de l’appareil en question.</span><span class="sxs-lookup"><span data-stu-id="f91be-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="f91be-179">Une atténuation ne résout pas les précédents événements de connexion à risque associés à l’identité ou à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="f91be-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="f91be-180">Pour limiter les connexions risquées automatiquement, vous pouvez configurer des stratégies de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f91be-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="f91be-181">Avec ce type de stratégie, vous prenez en compte le niveau de risque de l’utilisateur ou de la connexion pour bloquer les connexions à risque ou exiger une authentification multifacteur de la part de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="f91be-182">Ces mesures peuvent empêcher un cybercriminel d’exploiter une identité volée pour causer des dommages et vous donner le temps de sécuriser l’identité.</span><span class="sxs-lookup"><span data-stu-id="f91be-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="f91be-183">Stratégie de sécurité en matière de risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="f91be-183">Sign-in risk security policy</span></span>
<span data-ttu-id="f91be-184">Une stratégie en matière de risque à la connexion est une stratégie d’accès conditionnel consistant à évaluer le risque associé à une connexion spécifique et qui applique des mesures d’atténuation à partir de règles et de conditions prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="f91be-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="f91be-185">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1014.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="f91be-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="f91be-186">Azure AD Identity Protection vous aide à gérer l’atténuation des connexions à risque, en vous permettant d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91be-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="f91be-187">Définir les utilisateurs et les groupes auxquels la stratégie s’applique :</span><span class="sxs-lookup"><span data-stu-id="f91be-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="f91be-188">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1015.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="f91be-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="f91be-189">Définir le niveau de risque à la connexion (Faible, Moyen ou Élevé) qui déclenche la stratégie :</span><span class="sxs-lookup"><span data-stu-id="f91be-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="f91be-190">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1016.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="f91be-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="f91be-191">Définir les contrôles à appliquer lorsque la stratégie est déclenchée :</span><span class="sxs-lookup"><span data-stu-id="f91be-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="f91be-192">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1017.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="f91be-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="f91be-193">Basculer l’état de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="f91be-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="f91be-194">![Inscription à MFA](./media/active-directory-identityprotection/403.png "Inscription à MFA")</span><span class="sxs-lookup"><span data-stu-id="f91be-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="f91be-195">Examiner et évaluer l’impact d’un changement avant de l’appliquer :</span><span class="sxs-lookup"><span data-stu-id="f91be-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="f91be-196">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1018.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="f91be-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="f91be-197">Bon à savoir</span><span class="sxs-lookup"><span data-stu-id="f91be-197">What you need to know</span></span>
<span data-ttu-id="f91be-198">Vous pouvez configurer une stratégie de sécurité en matière de risque à la connexion pour exiger l’authentification multifacteur :</span><span class="sxs-lookup"><span data-stu-id="f91be-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="f91be-199">![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1017.png "Stratégie en matière de risque à la connexion")</span><span class="sxs-lookup"><span data-stu-id="f91be-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="f91be-200">Toutefois, pour des raisons de sécurité, ce paramètre s’applique uniquement aux utilisateurs qui ont déjà été inscrits pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="f91be-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="f91be-201">En cas d’obligation d’authentification multifacteur pour un utilisateur qui n’est pas encore inscrit pour l’authentification multifacteur, l’utilisateur est bloqué.</span><span class="sxs-lookup"><span data-stu-id="f91be-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="f91be-202">La meilleure pratique pour exiger une authentification multifacteur pour les connexions à risque consiste à :</span><span class="sxs-lookup"><span data-stu-id="f91be-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="f91be-203">Activer la [stratégie d’inscription à l’authentification multifacteur](#multi-factor-authentication-registration-policy) pour les utilisateurs concernés, et</span><span class="sxs-lookup"><span data-stu-id="f91be-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="f91be-204">Demander aux utilisateurs concernés de se connecter à une session ne présentant aucun risque pour s’inscrire à l’authentification MFA.</span><span class="sxs-lookup"><span data-stu-id="f91be-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="f91be-205">Suivre ces étapes permet de s’assurer que l’authentification multifacteur est requise pour une connexion à risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="f91be-206">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="f91be-206">Best practices</span></span>
<span data-ttu-id="f91be-207">La sélection d’un niveau de risque **Élevé** réduit la fréquence de déclenchement d’une stratégie et minimise l’impact sur les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f91be-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="f91be-208">Cependant, cela a pour effet d’exclure les connexions associées à un indicateur de risque **Faible** et **Moyen**. Par conséquent, il se peut qu’un cybercriminel soit en mesure d’exploiter une identité compromise.</span><span class="sxs-lookup"><span data-stu-id="f91be-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="f91be-209">Pour définir la stratégie</span><span class="sxs-lookup"><span data-stu-id="f91be-209">When setting the policy,</span></span>

* <span data-ttu-id="f91be-210">Excluez les utilisateurs qui ne sont pas inscrits/ne peuvent pas s’inscrire à l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="f91be-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="f91be-211">Excluez les utilisateurs situés dans des régions où l’activation de la stratégie n’est pas adaptée (par exemple, aucun accès au support technique).</span><span class="sxs-lookup"><span data-stu-id="f91be-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="f91be-212">Excluez les utilisateurs susceptibles de générer un grand nombre de faux positifs (développeurs, analystes de sécurité).</span><span class="sxs-lookup"><span data-stu-id="f91be-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="f91be-213">Utilisez un niveau de risque **Élevé** pendant le déploiement initial de la stratégie ou si vous devez minimiser la complexité pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="f91be-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="f91be-214">Utilisez un niveau de risque **Faible** si votre organisation nécessite une sécurité accrue.</span><span class="sxs-lookup"><span data-stu-id="f91be-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="f91be-215">La sélection d’un niveau de risque **Faible** complique la connexion pour les utilisateurs, mais renforce la sécurité.</span><span class="sxs-lookup"><span data-stu-id="f91be-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="f91be-216">Pour la plupart des organisations, nous recommandons de configurer un niveau de risque **Moyen** afin d’établir un juste équilibre entre facilité d’utilisation et sécurité.</span><span class="sxs-lookup"><span data-stu-id="f91be-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="f91be-217">La stratégie en matière de risque à la connexion :</span><span class="sxs-lookup"><span data-stu-id="f91be-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="f91be-218">est appliquée à l’ensemble du trafic de navigateur et des connexions utilisant une authentification moderne ;</span><span class="sxs-lookup"><span data-stu-id="f91be-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="f91be-219">n’est pas appliquée aux applications utilisant des protocoles de sécurité plus anciens en désactivant le point de terminaison WS-Trust sur le fournisseur d’identité fédérée, tels qu’ADFS.</span><span class="sxs-lookup"><span data-stu-id="f91be-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="f91be-220">La page **Événements à risque** de la console Identity Protection répertorie tous les événements :</span><span class="sxs-lookup"><span data-stu-id="f91be-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="f91be-221">auxquels cette stratégie a été appliquée ;</span><span class="sxs-lookup"><span data-stu-id="f91be-221">This policy was applied to</span></span>
* <span data-ttu-id="f91be-222">pour lesquels vous pouvez consulter l’activité afin de déterminer si la mesure était appropriée ou non.</span><span class="sxs-lookup"><span data-stu-id="f91be-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="f91be-223">Pour une obtenir une vue d’ensemble de l’expérience utilisateur, consultez :</span><span class="sxs-lookup"><span data-stu-id="f91be-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="f91be-224">Récupération de connexion à risque</span><span class="sxs-lookup"><span data-stu-id="f91be-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="f91be-225">Connexion à risque bloquée</span><span class="sxs-lookup"><span data-stu-id="f91be-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="f91be-226">Expériences de connexion avec Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="f91be-227">**Pour ouvrir la boîte de dialogue de configuration connexe**:</span><span class="sxs-lookup"><span data-stu-id="f91be-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="f91be-228">Dans le panneau **Azure AD Identity Protection**, dans la section **Configurer**, cliquez sur **Stratégie en matière de risque à la connexion**.</span><span class="sxs-lookup"><span data-stu-id="f91be-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="f91be-229">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1014.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="f91be-230">Utilisateurs associés à un indicateur de risque</span><span class="sxs-lookup"><span data-stu-id="f91be-230">Users flagged for risk</span></span>

<span data-ttu-id="f91be-231">Tous les [événements à risque](active-directory-identity-protection-risk-events.md) actifs détectés par Azure Active Directory pour un utilisateur alimentent un concept logique appelé « risque de l’utilisateur ».</span><span class="sxs-lookup"><span data-stu-id="f91be-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="f91be-232">Un utilisateur signalé comme présentant un risque indique qu’un compte d’utilisateur est susceptible d’avoir été compromis.</span><span class="sxs-lookup"><span data-stu-id="f91be-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Utilisateurs associés à un indicateur de risque](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="f91be-234">Niveau de risque d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91be-234">User risk level</span></span>

<span data-ttu-id="f91be-235">Le niveau de risque d’un utilisateur est une indication (Élevé, Moyen ou Faible) de la probabilité que l’identité de l’utilisateur ait été compromise.</span><span class="sxs-lookup"><span data-stu-id="f91be-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="f91be-236">Il est calculé en fonction des événements à risque associés à l’identité de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="f91be-237">L’état d’un événement à risque est soit **Actif**, soit **Fermé**.</span><span class="sxs-lookup"><span data-stu-id="f91be-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="f91be-238">Seuls les événements à risque qui sont **actifs** entrent dans le calcul du risque d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="f91be-239">Le niveau de risque d’un utilisateur est calculé à l’aide des données suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91be-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="f91be-240">Événements à risque actifs ayant un impact sur l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91be-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="f91be-241">Niveau de risque de ces événements</span><span class="sxs-lookup"><span data-stu-id="f91be-241">Risk level of these events</span></span>
* <span data-ttu-id="f91be-242">Application ou non de mesures de correction</span><span class="sxs-lookup"><span data-stu-id="f91be-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="f91be-243">![Risques des utilisateurs](./media/active-directory-identityprotection/1031.png "Risques des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="f91be-244">Vous pouvez utiliser les niveaux de risque des utilisateurs pour créer des stratégies d’accès conditionnel qui empêchent les utilisateurs à risque de se connecter ou les forcent à sécuriser leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f91be-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="f91be-245">Fermeture manuelle des événements à risque</span><span class="sxs-lookup"><span data-stu-id="f91be-245">Closing risk events manually</span></span>

<span data-ttu-id="f91be-246">Dans la plupart des cas, vous pouvez prendre des mesures de correction telles qu’une réinitialisation de mot de passe sécurisée pour fermer automatiquement les événements à risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="f91be-247">Toutefois, il se peut que cela ne soit pas toujours possible.</span><span class="sxs-lookup"><span data-stu-id="f91be-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="f91be-248">C’est par exemple le cas quand :</span><span class="sxs-lookup"><span data-stu-id="f91be-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="f91be-249">un utilisateur avec des événements à risque actifs a été supprimé ;</span><span class="sxs-lookup"><span data-stu-id="f91be-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="f91be-250">une enquête révèle qu’un événement à risque signalé a été effectué par l’utilisateur légitime.</span><span class="sxs-lookup"><span data-stu-id="f91be-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="f91be-251">Comme les événements à risque dont l’état est défini sur **Actif** entrent dans le calcul du risque des utilisateurs, vous pouvez avoir besoin de réduire manuellement un niveau de risque en fermant manuellement les événements à risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="f91be-252">Au cours de l’investigation, vous pouvez choisir d’effectuer n’importe laquelle des actions suivantes pour modifier l’état d’un événement à risque :</span><span class="sxs-lookup"><span data-stu-id="f91be-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="f91be-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="f91be-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="f91be-254">**Résoudre** : si après avoir examiné un événement à risque, vous avez pris une mesure de correction appropriée en dehors d’Identity Protection et pensez que l’événement à risque doit être considéré comme fermé, marquez l’événement comme résolu.</span><span class="sxs-lookup"><span data-stu-id="f91be-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="f91be-255">L’état des événements à risque résolus est défini sur Fermé et ces événements n’entrent plus dans le calcul du risque d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="f91be-256">**Marquer comme faux positif** : dans certains cas, il se peut qu’un événement à risque soit signalé à tort en tant que tel.</span><span class="sxs-lookup"><span data-stu-id="f91be-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="f91be-257">Vous pouvez réduire le nombre de ces événements en les marquant comme faux positifs.</span><span class="sxs-lookup"><span data-stu-id="f91be-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="f91be-258">Vous aiderez ainsi les algorithmes d’apprentissage automatique à améliorer la classification des événements similaires par la suite.</span><span class="sxs-lookup"><span data-stu-id="f91be-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="f91be-259">L’état des événements marqués comme faux positifs est défini sur **Fermé** et ces événements n’entrent plus dans le calcul du risque de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="f91be-260">**Ignorer** : si vous n’avez pris aucune mesure de correction, mais que vous souhaitez que l’événement à risque soit supprimé de la liste active, vous pouvez choisir de l’ignorer. Son état sera alors défini sur Fermé.</span><span class="sxs-lookup"><span data-stu-id="f91be-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="f91be-261">Les événements ignorés n’entrent plus dans le calcul du risque d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="f91be-262">Cette option doit uniquement être utilisée dans des circonstances inhabituelles.</span><span class="sxs-lookup"><span data-stu-id="f91be-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="f91be-263">**Réactiver** : les événements à risque qui ont été fermés manuellement (en choisissant **Résoudre**, **Marquer comme faux positif** ou **Ignore**) peuvent être réactivés. Leur statut est alors défini à nouveau sur **Actif**.</span><span class="sxs-lookup"><span data-stu-id="f91be-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="f91be-264">Les événements à risque réactivés contribuent au calcul du niveau de risque d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="f91be-265">Les événements à risque fermés à l’aide d’une mesure de correction (telle qu’une réinitialisation de mot de passe sécurisée) ne peuvent pas être réactivés.</span><span class="sxs-lookup"><span data-stu-id="f91be-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="f91be-266">**Pour ouvrir la boîte de dialogue de configuration connexe**:</span><span class="sxs-lookup"><span data-stu-id="f91be-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="f91be-267">Dans le panneau **Azure AD Identity Protection**, sous **Examiner**, cliquez sur **Événements à risque**.</span><span class="sxs-lookup"><span data-stu-id="f91be-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="f91be-268">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1002.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="f91be-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="f91be-269">Dans la liste **Événements à risque** , cliquez sur un risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="f91be-270">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1003.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="f91be-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="f91be-271">Dans le panneau Risque, cliquez avec le bouton droit sur un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="f91be-272">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1004.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="f91be-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="f91be-273">Fermeture manuelle de tous les événements à risque pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91be-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="f91be-274">Au lieu de fermer manuellement les événements à risque pour chaque utilisateur, Azure Active Directory Identity Protection propose une méthode permettant de fermer tous les événements pour un utilisateur en un seul clic.</span><span class="sxs-lookup"><span data-stu-id="f91be-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="f91be-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="f91be-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="f91be-276">Lorsque vous cliquez sur **Ignorer tous les événements**, tous les événements sont fermés et l’utilisateur concerné n’est plus exposé.</span><span class="sxs-lookup"><span data-stu-id="f91be-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="f91be-277">Correction des événements à risque d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91be-277">Remediating user risk events</span></span>

<span data-ttu-id="f91be-278">Une correction est une mesure visant à sécuriser une identité ou un appareil déjà identifié comme potentiellement ou effectivement compromis.</span><span class="sxs-lookup"><span data-stu-id="f91be-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="f91be-279">Une mesure de correction permet de rétablir la sécurité de l’identité ou de l’appareil et de résoudre les anciens événements à risque associés à l’identité ou à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="f91be-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="f91be-280">Pour corriger les événements à risque d’un utilisateur, vous pouvez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="f91be-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="f91be-281">Effectuez une réinitialisation de mot de passe sécurisée pour corriger manuellement les événements à risque de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="f91be-282">Configurez une stratégie de sécurité en matière de risque des utilisateurs pour atténuer ou corriger automatiquement les événements à risque de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="f91be-283">Réimager l’appareil infecté.</span><span class="sxs-lookup"><span data-stu-id="f91be-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="f91be-284">Réinitialisation manuelle et sécurisée du mot de passe</span><span class="sxs-lookup"><span data-stu-id="f91be-284">Manual secure password reset</span></span>
<span data-ttu-id="f91be-285">Une réinitialisation de mot de passe sécurisée est une mesure de correction efficace pour de nombreux événements à risque. Lorsqu’elle est effectuée, ces événements à risque sont fermés et le niveau de risque de l’utilisateur correspondant recalculé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f91be-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="f91be-286">Vous pouvez utiliser le tableau de bord d’Identity Protection afin de lancer une réinitialisation de mot de passe pour un utilisateur à risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="f91be-287">La boîte de dialogue connexe fournit deux méthodes différentes pour réinitialiser le mot de passe :</span><span class="sxs-lookup"><span data-stu-id="f91be-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="f91be-288">**Réinitialiser le mot de passe** : sélectionnez **Demander à l’utilisateur de réinitialiser son mot de passe** pour permettre à l’utilisateur de récupérer lui-même son compte s’il s’est inscrit à l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="f91be-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="f91be-289">La prochaine fois que l’utilisateur se connectera, il devra résoudre une demande d’authentification multifacteur, puis sera obligé de changer le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f91be-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="f91be-290">Cette option n’est pas disponible si le compte d’utilisateur n’est pas déjà inscrit à l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="f91be-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="f91be-291">**Mot de passe temporaire** : sélectionnez **Générer un mot de passe temporaire** pour invalider immédiatement le mot de passe existant et créer un nouveau mot de passe temporaire pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="f91be-292">Envoyez le nouveau mot de passe temporaire à une autre adresse de messagerie de l’utilisateur ou au responsable de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="f91be-293">Étant donné que le mot de passe est temporaire, l’utilisateur sera invité à changer le mot de passe lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="f91be-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="f91be-294">![Stratégie](./media/active-directory-identityprotection/1005.png "Stratégie")</span><span class="sxs-lookup"><span data-stu-id="f91be-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="f91be-295">**Pour ouvrir la boîte de dialogue de configuration connexe**:</span><span class="sxs-lookup"><span data-stu-id="f91be-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="f91be-296">Dans le panneau **Azure AD Identity Protection**, cliquez sur **Utilisateurs associés à un indicateur de risque**.</span><span class="sxs-lookup"><span data-stu-id="f91be-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="f91be-297">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1006.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="f91be-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="f91be-298">Dans la liste des utilisateurs, sélectionnez un utilisateur comportant au moins un risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="f91be-299">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1007.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="f91be-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="f91be-300">Dans le panneau Utilisateur, cliquez sur **Réinitialiser le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f91be-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="f91be-301">![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1008.png "Réinitialisation manuelle du mot de passe")</span><span class="sxs-lookup"><span data-stu-id="f91be-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="f91be-302">Stratégie de sécurité en matière de risque des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f91be-302">User risk security policy</span></span>
<span data-ttu-id="f91be-303">Une stratégie de sécurité en matière de risque des utilisateurs est une stratégie d’accès conditionnel qui évalue le niveau de risque d’un utilisateur spécifique et applique des mesures de correction et d’atténuation en fonction de conditions et de règles prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="f91be-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="f91be-304">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1009.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="f91be-305">Azure AD Identity Protection vous aide à gérer les mesures de correction et d’atténuation pour les utilisateurs associés à un indicateur de risque, en vous permettant d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91be-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="f91be-306">Définir les utilisateurs et les groupes auxquels la stratégie s’applique :</span><span class="sxs-lookup"><span data-stu-id="f91be-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="f91be-307">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1010.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="f91be-308">Définir le niveau de risque d’un utilisateur (Faible, Moyen ou Élevé) qui déclenche la stratégie :</span><span class="sxs-lookup"><span data-stu-id="f91be-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="f91be-309">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1011.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="f91be-310">Définir les contrôles à appliquer lorsque la stratégie est déclenchée :</span><span class="sxs-lookup"><span data-stu-id="f91be-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="f91be-311">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1012.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="f91be-312">Basculer l’état de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="f91be-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="f91be-313">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/403.png "Inscription à MFA")</span><span class="sxs-lookup"><span data-stu-id="f91be-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="f91be-314">Examiner et évaluer l’impact d’un changement avant de l’appliquer :</span><span class="sxs-lookup"><span data-stu-id="f91be-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="f91be-315">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1013.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="f91be-316">La sélection d’un niveau de risque **Élevé** réduit la fréquence de déclenchement d’une stratégie et minimise l’impact sur les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f91be-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="f91be-317">Cependant, cela a pour effet d’exclure les utilisateurs associés à un indicateur de risque **Faible** et **Moyen**. Par conséquent, il se peut que des identités ou des appareils déjà identifiés comme potentiellement ou effectivement compromis ne soient pas sécurisés.</span><span class="sxs-lookup"><span data-stu-id="f91be-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="f91be-318">Pour définir la stratégie</span><span class="sxs-lookup"><span data-stu-id="f91be-318">When setting the policy,</span></span>

* <span data-ttu-id="f91be-319">Excluez les utilisateurs susceptibles de générer un grand nombre de faux positifs (développeurs, analystes de sécurité).</span><span class="sxs-lookup"><span data-stu-id="f91be-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="f91be-320">Excluez les utilisateurs situés dans des régions où l’activation de la stratégie n’est pas adaptée (par exemple, aucun accès au support technique).</span><span class="sxs-lookup"><span data-stu-id="f91be-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="f91be-321">Utilisez un niveau de risque **Élevé** pendant le déploiement initial de la stratégie ou si vous devez minimiser la complexité pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="f91be-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="f91be-322">Utilisez un niveau de risque **Faible** si votre organisation nécessite une sécurité accrue.</span><span class="sxs-lookup"><span data-stu-id="f91be-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="f91be-323">La sélection d’un niveau de risque **Faible** complique la connexion pour les utilisateurs, mais renforce la sécurité.</span><span class="sxs-lookup"><span data-stu-id="f91be-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="f91be-324">Pour la plupart des organisations, nous recommandons de configurer un niveau de risque **Moyen** afin d’établir un juste équilibre entre facilité d’utilisation et sécurité.</span><span class="sxs-lookup"><span data-stu-id="f91be-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="f91be-325">Pour une obtenir une vue d’ensemble de l’expérience utilisateur, consultez :</span><span class="sxs-lookup"><span data-stu-id="f91be-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="f91be-326">[Flux de récupération de compte compromis](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="f91be-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="f91be-327">[Flux de compte compromis bloqué](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="f91be-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="f91be-328">**Pour ouvrir la boîte de dialogue de configuration connexe**:</span><span class="sxs-lookup"><span data-stu-id="f91be-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="f91be-329">Dans le panneau **Azure AD Identity Protection**, dans la section **Configurer**, cliquez sur **Stratégie de risque d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f91be-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="f91be-330">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1009.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="f91be-331">Atténuation des événements à risque d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91be-331">Mitigating user risk events</span></span>
<span data-ttu-id="f91be-332">Les administrateurs peuvent définir une stratégie de sécurité en matière de risque des utilisateurs pour bloquer les utilisateurs lors de la connexion selon le niveau de risque.</span><span class="sxs-lookup"><span data-stu-id="f91be-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="f91be-333">Le blocage d’une connexion :</span><span class="sxs-lookup"><span data-stu-id="f91be-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="f91be-334">empêche la génération de nouveaux événements à risque pour l’utilisateur concerné ;</span><span class="sxs-lookup"><span data-stu-id="f91be-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="f91be-335">permet aux administrateurs de corriger manuellement les événements à risques affectant l’identité de l’utilisateur pour sécuriser à nouveau cette dernière.</span><span class="sxs-lookup"><span data-stu-id="f91be-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="f91be-336">Stratégie d’inscription à l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="f91be-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="f91be-337">Azure Multi-Factor Authentication est une méthode permettant de vérifier votre identité qui requiert l’utilisation d’autres méthodes que le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f91be-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="f91be-338">Ce service fournit une deuxième couche de sécurité pour les connexions et les transactions de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91be-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="f91be-339">Nous vous recommandons d’exiger l’authentification multifacteur d’Azure des connexions des utilisateurs pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91be-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="f91be-340">Elle fournit une authentification renforcée avec un éventail d’options de vérification simples.</span><span class="sxs-lookup"><span data-stu-id="f91be-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="f91be-341">Elle joue un rôle clé dans la préparation de votre organisation pour protéger et récupérer les comptes compromis.</span><span class="sxs-lookup"><span data-stu-id="f91be-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="f91be-342">![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1019.png "Stratégie en matière de risque des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f91be-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="f91be-343">Pour plus d’informations, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f91be-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="f91be-344">Azure AD Identity Protection vous permet de gérer le déploiement de l’inscription à l’authentification multifacteur en configurant une stratégie qui vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91be-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="f91be-345">Définir les utilisateurs et les groupes auxquels la stratégie s’applique :</span><span class="sxs-lookup"><span data-stu-id="f91be-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="f91be-346">![Stratégie MFA](./media/active-directory-identityprotection/1020.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="f91be-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="f91be-347">Définir les contrôles à appliquer lorsque la stratégie est déclenchée :</span><span class="sxs-lookup"><span data-stu-id="f91be-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="f91be-348">![Stratégie MFA](./media/active-directory-identityprotection/1021.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="f91be-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="f91be-349">Basculer l’état de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="f91be-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="f91be-350">![Stratégie MFA](./media/active-directory-identityprotection/403.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="f91be-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="f91be-351">Afficher l’état d’inscription actuel :</span><span class="sxs-lookup"><span data-stu-id="f91be-351">View the current registration status:</span></span>

    <span data-ttu-id="f91be-352">![Stratégie MFA](./media/active-directory-identityprotection/1022.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="f91be-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="f91be-353">Pour une obtenir une vue d’ensemble de l’expérience utilisateur, consultez :</span><span class="sxs-lookup"><span data-stu-id="f91be-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="f91be-354">[Processus d’inscription à l’authentification multifacteur](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="f91be-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="f91be-355">[Expériences de connexion avec Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="f91be-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="f91be-356">**Pour ouvrir la boîte de dialogue de configuration connexe**:</span><span class="sxs-lookup"><span data-stu-id="f91be-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="f91be-357">Dans le panneau **Azure AD Identity Protection**, dans la section **Configurer**, cliquez sur **Inscription à l’authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="f91be-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="f91be-358">![Stratégie MFA](./media/active-directory-identityprotection/1019.png "Stratégie MFA")</span><span class="sxs-lookup"><span data-stu-id="f91be-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="f91be-359">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f91be-359">Next steps</span></span>
* [<span data-ttu-id="f91be-360">Channel 9 : Azure AD and Identity Show: Identity Protection Preview (Émission sur Azure AD et l’identité : présentation d’Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="f91be-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="f91be-361">Activer Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="f91be-362">Vulnérabilités détectées par Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="f91be-363">Événements à risque dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f91be-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="f91be-364">Notifications d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="f91be-365">Manuel d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="f91be-366">Glossaire d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="f91be-367">Expériences de connexion avec Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f91be-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="f91be-368">Azure Active Directory Identity Protection - Déblocage des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f91be-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="f91be-369">Prise en main d’Azure Active Directory Identity Protection et de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f91be-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
