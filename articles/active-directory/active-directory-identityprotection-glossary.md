---
title: "Glossaire d’Azure Active Directory Identity Protection | Microsoft Docs"
description: "Glossaire d’Azure Active Directory Identity Protection"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité, glossaire"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2cf64925cff9a78cf83532a1cfd231f7a1d98304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="bdd7b-104">Glossaire d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bdd7b-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="bdd7b-105">À risque (utilisateur)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-105">At risk (User)</span></span>
<span data-ttu-id="bdd7b-106">Utilisateur associé à un ou plusieurs événements à risque actifs.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="bdd7b-107">Emplacement de connexion atypique</span><span class="sxs-lookup"><span data-stu-id="bdd7b-107">Atypical sign-in location</span></span>
<span data-ttu-id="bdd7b-108">Connexion effectuée depuis une zone géographique inhabituelle pour l’utilisateur spécifique, pour des utilisateurs similaires ou pour le client.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="bdd7b-109">Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bdd7b-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="bdd7b-110">Module de sécurité d’Azure Active Directory offrant une vue consolidée des événements à risque et des vulnérabilités potentielles qui affectent les identités d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="bdd7b-111">Accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="bdd7b-111">Conditional access</span></span>
<span data-ttu-id="bdd7b-112">Stratégie de sécurisation des accès aux ressources.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-112">A policy for securing access to resources.</span></span> <span data-ttu-id="bdd7b-113">Les règles d’accès conditionnel sont stockées dans Azure Active Directory et sont évaluées par Azure AD avant tout octroi d’accès à la ressource.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span></span>  <span data-ttu-id="bdd7b-114">Il existe, par exemple, des règles de restriction d’accès en fonction de l’emplacement de l’utilisateur, de l’intégrité de l’appareil ou de la méthode d’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="bdd7b-115">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="bdd7b-115">Credentials</span></span>
<span data-ttu-id="bdd7b-116">Informations contenant à la fois une identification et une preuve d’identification et qui permettent l’accès aux ressources locales et réseau.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span></span> <span data-ttu-id="bdd7b-117">Les noms d’utilisateur et mots de passe, les cartes à puce et les certificats sont des exemples d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="bdd7b-118">Événement</span><span class="sxs-lookup"><span data-stu-id="bdd7b-118">Event</span></span>
<span data-ttu-id="bdd7b-119">Enregistrement d’une activité dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="bdd7b-120">Faux positif (événement à risque)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-120">False-positive (risk event)</span></span>
<span data-ttu-id="bdd7b-121">État d’un événement à risque défini manuellement par un utilisateur du service Identity Protection, indiquant que l’événement à risque a été examiné et marqué à tort comme un événement à risque.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="bdd7b-122">Identité</span><span class="sxs-lookup"><span data-stu-id="bdd7b-122">Identity</span></span>
<span data-ttu-id="bdd7b-123">Personne ou entité devant faire l’objet d’une vérification au moyen d’une authentification basée sur certains critères, tels qu’un mot de passe ou un certificat.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="bdd7b-124">Événement de risque d’identité</span><span class="sxs-lookup"><span data-stu-id="bdd7b-124">Identity risk event</span></span>
<span data-ttu-id="bdd7b-125">Événement AAD ayant été marqué comme anormal par le service Identity Protection et qui peut impliquer la corruption d’une identité.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="bdd7b-126">Ignoré (événement à risque)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-126">Ignored (risk event)</span></span>
<span data-ttu-id="bdd7b-127">État d’un événement à risque défini manuellement par un utilisateur du service Identity Protection et qui indique que l’événement à risque a été clos sans mise en place d’une action corrective.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="bdd7b-128">Déplacement impossible à partir d’emplacements inhabituels</span><span class="sxs-lookup"><span data-stu-id="bdd7b-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="bdd7b-129">Événement à risque déclenché lorsque le service détecte deux connexions du même utilisateur, dont au moins une effectuée depuis un emplacement inhabituel, et pour lesquelles le délai entre les connexions est inférieur au temps minimum nécessaire pour se déplacer physiquement entre ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="bdd7b-130">Investigation</span><span class="sxs-lookup"><span data-stu-id="bdd7b-130">Investigation</span></span>
<span data-ttu-id="bdd7b-131">Processus consistant à vérifier les activités, les journaux et les autres informations pertinentes concernant un événement à risque, dans le but de déterminer la nécessité d’appliquer des mesures de correction ou d’atténuation, de comprendre si l’identité a été corrompue et de quelle manière, et d’identifier la manière dont l’identité corrompue a été exploitée.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="bdd7b-132">Informations d’identification divulguées</span><span class="sxs-lookup"><span data-stu-id="bdd7b-132">Leaked credentials</span></span>
<span data-ttu-id="bdd7b-133">Événement à risque déclenché lorsque nos chercheurs découvrent que les informations d’identification de l’utilisateur actuel (nom d’utilisateur et mot de passe) sont publiées dans le web invisible.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="bdd7b-134">Atténuation</span><span class="sxs-lookup"><span data-stu-id="bdd7b-134">Mitigation</span></span>
<span data-ttu-id="bdd7b-135">Action visant à limiter ou éliminer la probabilité qu’un pirate exploite une identité ou un appareil corrompu, mais qui ne permet pas de rétablir la sécurité de l’identité ou de l’appareil en question.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="bdd7b-136">Une atténuation ne résout pas les précédents événements à risque associés à l’identité ou à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-136">A mitigation does not resolve previous risk events associated with the identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="bdd7b-137">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="bdd7b-137">Multi-factor authentication</span></span>
<span data-ttu-id="bdd7b-138">Méthode d’authentification imposant l’utilisation d’au moins deux modes d’authentification, par exemple un objet en la possession de l’utilisateur (certificat), une information connue de l’utilisateur (noms d’utilisateur, mots de passe ou phrases secrètes), des attributs physiques (empreinte numérique) ou encore des attributs personnels (signature personnelle).</span><span class="sxs-lookup"><span data-stu-id="bdd7b-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="bdd7b-139">Détection en mode hors connexion</span><span class="sxs-lookup"><span data-stu-id="bdd7b-139">Offline detection</span></span>
<span data-ttu-id="bdd7b-140">Détection d’anomalies et évaluation du risque d’un événement, tel qu’une tentative de connexion consécutive à l’événement, concernant un événement qui a déjà eu lieu.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="bdd7b-141">Condition de stratégie</span><span class="sxs-lookup"><span data-stu-id="bdd7b-141">Policy condition</span></span>
<span data-ttu-id="bdd7b-142">Partie d’une stratégie de sécurité qui définit les entités (groupes, utilisateurs, applications, plateformes d’appareils, états d’appareils, plages d’adresses IP, types de client) incluses dans la stratégie ou qui en sont exclues.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="bdd7b-143">Règle de stratégie</span><span class="sxs-lookup"><span data-stu-id="bdd7b-143">Policy rule</span></span>
<span data-ttu-id="bdd7b-144">Partie d’une stratégie de sécurité qui décrit les circonstances entraînant le déclenchement de la stratégie ainsi que les actions exécutées lors du déclenchement de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="bdd7b-145">Prévention</span><span class="sxs-lookup"><span data-stu-id="bdd7b-145">Prevention</span></span>
<span data-ttu-id="bdd7b-146">Action visant à protéger l’organisation des dommages liés à l’utilisation abusive d’une identité ou d’un appareil potentiellement ou effectivement corrompu.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span></span> <span data-ttu-id="bdd7b-147">Une action de prévention ne garantit nullement la sécurité de l’appareil ou de l’identité, de même qu’elle n’a aucun effet sur les événements à risque passés.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="bdd7b-148">Privilégié (utilisateur)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-148">Privileged (user)</span></span>
<span data-ttu-id="bdd7b-149">Utilisateur qui, au moment d’un événement à risque, possédait des autorisations d’administration permanentes ou temporaires sur une ou plusieurs ressources dans Azure Active Directory. Il peut s’agir, par exemple, d’un administrateur global, d’un administrateur de facturation, d’un administrateur de service, d’un administrateur d’utilisateurs ou encore d’un administrateur de mots de passe.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="bdd7b-150">Temps réel</span><span class="sxs-lookup"><span data-stu-id="bdd7b-150">Real-time</span></span>
<span data-ttu-id="bdd7b-151">Voir « Détection en temps réel ».</span><span class="sxs-lookup"><span data-stu-id="bdd7b-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="bdd7b-152">Détection en temps réel</span><span class="sxs-lookup"><span data-stu-id="bdd7b-152">Real-time detection</span></span>
<span data-ttu-id="bdd7b-153">Détection d’anomalies et évaluation du risque d’un événement, tel qu’une tentative de connexion, effectuée avant d’autoriser la poursuite de la progression d’un événement.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="bdd7b-154">Corrigé (événement à risque)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-154">Remediated (risk event)</span></span>
<span data-ttu-id="bdd7b-155">État d’un événement à risque défini automatiquement par le service Identity Protection et qui indique que l’événement à risque a été résolu grâce à la mise en place d’une action corrective standard pour ce type d’événement à risque.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span></span> <span data-ttu-id="bdd7b-156">Par exemple, lors de la réinitialisation du mot de passe de l’utilisateur, de nombreux événements à risque indiquant une corruption de l’ancien mot de passe seront résolus automatiquement.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="bdd7b-157">Correction</span><span class="sxs-lookup"><span data-stu-id="bdd7b-157">Remediation</span></span>
<span data-ttu-id="bdd7b-158">Action visant à sécuriser une identité ou un appareil déjà identifié comme potentiellement ou effectivement corrompu.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span></span> <span data-ttu-id="bdd7b-159">Une mesure de correction permet de rétablir la sécurité de l’identité ou de l’appareil et de résoudre les anciens événements à risque associés à l’identité ou à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="bdd7b-160">Résolu (événement à risque)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-160">Resolved (risk event)</span></span>
<span data-ttu-id="bdd7b-161">État d’un événement à risque défini manuellement par un utilisateur du service Identity Protection qui indique que l’utilisateur a exécuté une action corrective appropriée en dehors d’Identity Protection et que l’événement à risque doit être considéré comme clos.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="bdd7b-162">État d’un événement à risque</span><span class="sxs-lookup"><span data-stu-id="bdd7b-162">Risk event status</span></span>
<span data-ttu-id="bdd7b-163">Propriété d’un événement à risque qui indique si l’événement est actif ou, s’il est clos, la raison de cet état.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="bdd7b-164">Type d’événement à risque</span><span class="sxs-lookup"><span data-stu-id="bdd7b-164">Risk event type</span></span>
<span data-ttu-id="bdd7b-165">Catégorie de l’événement à risque indiquant le type d’anomalie à l’origine de l’événement à risque.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="bdd7b-166">Niveau de risque (événement à risque)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-166">Risk level (risk event)</span></span>
<span data-ttu-id="bdd7b-167">Indication (élevée, moyenne ou faible) de la gravité de l’événement à risque, visant à aider les utilisateurs d’Identity Protection à hiérarchiser les actions à entreprendre afin de réduire le risque auquel s’expose leur organisation.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="bdd7b-168">Niveau de risque (connexion)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-168">Risk level (sign-in)</span></span>
<span data-ttu-id="bdd7b-169">Indication (élevée, moyenne ou faible) indiquant la probabilité qu’un tiers tente d’utiliser l’identité de l’utilisateur dans le cadre d’une connexion spécifique.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="bdd7b-170">Niveau de risque (compromission de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-170">Risk level (user compromise)</span></span>
<span data-ttu-id="bdd7b-171">Indication (élevée, moyenne ou faible) de la probabilité de corruption d’une identité.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="bdd7b-172">Niveau de risque (vulnérabilité)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="bdd7b-173">Indication (élevée, moyenne ou faible) de la gravité de la vulnérabilité, visant à aider les utilisateurs d’Identity Protection à hiérarchiser les actions à entreprendre afin de réduire le risque auquel s’expose leur organisation.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="bdd7b-174">Sécurisé (identité)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-174">Secure (identity)</span></span>
<span data-ttu-id="bdd7b-175">Application d’une mesure corrective (par exemple, changement de mot de passe ou réimageage d’un ordinateur) dans le but de rétablir la sécurité d’une identité potentiellement corrompue.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="bdd7b-176">Stratégie de sécurité</span><span class="sxs-lookup"><span data-stu-id="bdd7b-176">Security policy</span></span>
<span data-ttu-id="bdd7b-177">Ensemble de règles et conditions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="bdd7b-178">Une stratégie peut être appliquée à des entités, telles que des utilisateurs, groupes, applications, appareils, plateformes d’appareils, états d’appareils, plages d’adresses IP et types de clients Auth2.0.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="bdd7b-179">Lorsqu’une stratégie est activée, elle est évaluée chaque fois qu’un jeton est généré pour une ressource sur une entité incluse dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="bdd7b-180">Se connecter (v)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-180">Sign in (v)</span></span>
<span data-ttu-id="bdd7b-181">Processus d’authentification d’une identité dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-181">To authenticate to an identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="bdd7b-182">Connexion (n)</span><span class="sxs-lookup"><span data-stu-id="bdd7b-182">Sign-in (n)</span></span>
<span data-ttu-id="bdd7b-183">Processus ou action d’authentification d’une identité dans Azure Active Directory et événement qui capture cette opération.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="bdd7b-184">Connexion à partir d’une adresse IP anonyme</span><span class="sxs-lookup"><span data-stu-id="bdd7b-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="bdd7b-185">Événement à risque déclenché après une réussite de connexion à partir d’une adresse IP ayant été identifiée comme adresse IP proxy anonyme.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="bdd7b-186">Connexion à partir d’un appareil infecté</span><span class="sxs-lookup"><span data-stu-id="bdd7b-186">Sign-in from infected device</span></span>
<span data-ttu-id="bdd7b-187">Événement à risque déclenché lors d’une connexion provenant d’une adresse IP utilisée par un ou plusieurs appareils corrompus qui tentent activement de communiquer avec un serveur robot.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="bdd7b-188">Connexion à partir d’une adresse IP affichant une activité suspecte</span><span class="sxs-lookup"><span data-stu-id="bdd7b-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="bdd7b-189">Événement à risque déclenché après une réussite de connexion à partir d’une adresse IP associée à un grand nombre de tentatives de connexion effectuées pendant une courte période sur plusieurs comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="bdd7b-190">Connexion à partir d’un emplacement inconnu</span><span class="sxs-lookup"><span data-stu-id="bdd7b-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="bdd7b-191">Événement à risque déclenché lorsqu’un utilisateur parvient à se connecter depuis un nouvel emplacement (adresse IP, latitude/longitude et ASN).</span><span class="sxs-lookup"><span data-stu-id="bdd7b-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="bdd7b-192">Risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="bdd7b-192">Sign-in risk</span></span>
<span data-ttu-id="bdd7b-193">Voir « Niveau de risque (connexion) »</span><span class="sxs-lookup"><span data-stu-id="bdd7b-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="bdd7b-194">Stratégie en matière de risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="bdd7b-194">Sign-in risk policy</span></span>
<span data-ttu-id="bdd7b-195">Stratégie d’accès conditionnel consistant à évaluer le risque associé à une connexion spécifique et qui applique des mesures d’atténuation à partir de règles et de conditions prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="bdd7b-196">Risque de compromission de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bdd7b-196">User compromise risk</span></span>
<span data-ttu-id="bdd7b-197">Voir « Niveau de risque (compromission de l’utilisateur) »</span><span class="sxs-lookup"><span data-stu-id="bdd7b-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="bdd7b-198">Risque de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bdd7b-198">User risk</span></span>
<span data-ttu-id="bdd7b-199">Voir « Niveau de risque (compromission de l’utilisateur) ».</span><span class="sxs-lookup"><span data-stu-id="bdd7b-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="bdd7b-200">Stratégie de risque d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bdd7b-200">User risk policy</span></span>
<span data-ttu-id="bdd7b-201">Stratégie d’accès conditionnel consistant à évaluer la connexion et qui applique des mesures d’atténuation à partir de règles et de conditions prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="bdd7b-202">Utilisateurs associés à un indicateur de risque</span><span class="sxs-lookup"><span data-stu-id="bdd7b-202">Users flagged for risk</span></span>
<span data-ttu-id="bdd7b-203">Utilisateurs associés à des événements à risque actifs ou corrigés</span><span class="sxs-lookup"><span data-stu-id="bdd7b-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="bdd7b-204">Vulnérabilité</span><span class="sxs-lookup"><span data-stu-id="bdd7b-204">Vulnerability</span></span>
<span data-ttu-id="bdd7b-205">Configuration ou condition dans Azure Active Directory qui rend l’annuaire vulnérable aux attaques ou aux menaces.</span><span class="sxs-lookup"><span data-stu-id="bdd7b-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="bdd7b-206">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bdd7b-206">See also</span></span>
* [<span data-ttu-id="bdd7b-207">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bdd7b-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

