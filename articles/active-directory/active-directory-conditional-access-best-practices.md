---
title: "Meilleures pratiques l’accès conditionnel dans Azure Active Directory | Microsoft Docs"
description: "Découvrez-en davantage sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel."
services: active-directory
keywords: "accès conditionnel aux applications, accès conditionnel à Azure AD, accès sécurisé aux ressources d’entreprise, stratégies d’accès conditionnel"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="d5444-104">Meilleures pratiques l’accès conditionnel dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5444-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="d5444-105">Cette rubrique vous fournit des informations sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="d5444-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="d5444-106">Avant de lire cette rubrique, vous devez vous familiariser avec les concepts et la terminologie décrits dans [Accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d5444-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="d5444-107">Ce que vous devez savoir</span><span class="sxs-lookup"><span data-stu-id="d5444-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="d5444-108">Qu’est-ce qui est nécessaire pour faire fonctionner une stratégie ?</span><span class="sxs-lookup"><span data-stu-id="d5444-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="d5444-109">Lorsque vous créez une stratégie, aucun utilisateur, groupe, application ou contrôle d’accès n’est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d5444-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Applications cloud](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="d5444-111">Pour que votre stratégie fonctionne, vous devez configurer ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d5444-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="d5444-112">Quoi</span><span class="sxs-lookup"><span data-stu-id="d5444-112">What</span></span>           | <span data-ttu-id="d5444-113">Comment</span><span class="sxs-lookup"><span data-stu-id="d5444-113">How</span></span>                                  | <span data-ttu-id="d5444-114">Pourquoi</span><span class="sxs-lookup"><span data-stu-id="d5444-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="d5444-115">**Applications cloud**</span><span class="sxs-lookup"><span data-stu-id="d5444-115">**Cloud apps**</span></span> |<span data-ttu-id="d5444-116">Vous devez sélectionner une ou plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="d5444-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="d5444-117">L’objectif d’une stratégie d’accès conditionnel est de vous permettre d’ajuster la manière dont les utilisateurs autorisés peuvent accéder à vos applications.</span><span class="sxs-lookup"><span data-stu-id="d5444-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="d5444-118">**Utilisateurs et groupes**</span><span class="sxs-lookup"><span data-stu-id="d5444-118">**Users and groups**</span></span> | <span data-ttu-id="d5444-119">Vous devez sélectionner au moins un utilisateur ou groupe autorisé à accéder aux applications cloud sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="d5444-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="d5444-120">Une stratégie d’accès conditionnel, à laquelle aucun utilisateur ou groupe n’est affecté, n’est jamais déclenchée.</span><span class="sxs-lookup"><span data-stu-id="d5444-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="d5444-121">**Contrôles d’accès**</span><span class="sxs-lookup"><span data-stu-id="d5444-121">**Access controls**</span></span> | <span data-ttu-id="d5444-122">Vous devez sélectionner au moins un contrôle d'accès.</span><span class="sxs-lookup"><span data-stu-id="d5444-122">You need to select at least one access control.</span></span> | <span data-ttu-id="d5444-123">Votre processeur de stratégies doit savoir que faire si vos conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="d5444-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="d5444-124">En plus de ces exigences de base, dans de nombreux cas, vous devez également configurer une condition.</span><span class="sxs-lookup"><span data-stu-id="d5444-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="d5444-125">Si une stratégie peut fonctionner sans condition configurée, les conditions constituent un facteur déterminant pour l’ajustement précis de l’accès à vos applications.</span><span class="sxs-lookup"><span data-stu-id="d5444-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![Applications cloud](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="d5444-127">Comment les affectations sont-elles évaluées ?</span><span class="sxs-lookup"><span data-stu-id="d5444-127">How are assignments evaluated?</span></span>

<span data-ttu-id="d5444-128">Toutes les attributions sont reliées par l’opérateur logique **AND**.</span><span class="sxs-lookup"><span data-stu-id="d5444-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="d5444-129">Si vous configurez plusieurs affectations, elles doivent toutes être satisfaites pour que la stratégie soit déclenchée.</span><span class="sxs-lookup"><span data-stu-id="d5444-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="d5444-130">Pour configurer une condition d’emplacement applicable à toutes les connexions non établies depuis le réseau de votre organisation, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d5444-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="d5444-131">inclure **tous les emplacements**,</span><span class="sxs-lookup"><span data-stu-id="d5444-131">Including **All locations**</span></span>
- <span data-ttu-id="d5444-132">exclure **toutes les adresses IP approuvées**.</span><span class="sxs-lookup"><span data-stu-id="d5444-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="d5444-133">Que se passe-t-il si vous avez configuré des stratégies dans le portail Azure Classic et le portail Azure ?</span><span class="sxs-lookup"><span data-stu-id="d5444-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="d5444-134">Azure Active Directory applique les deux stratégies et l’utilisateur n’obtient l’accès que si toutes les conditions requises sont remplies.</span><span class="sxs-lookup"><span data-stu-id="d5444-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="d5444-135">Que se passe-t-il si vous avez des stratégies dans le portail Intune Silverlight et le portail Azure ?</span><span class="sxs-lookup"><span data-stu-id="d5444-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="d5444-136">Azure Active Directory applique les deux stratégies et l’utilisateur n’obtient l’accès que si toutes les conditions requises sont remplies.</span><span class="sxs-lookup"><span data-stu-id="d5444-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="d5444-137">Que se passe-t-il si j’ai configuré plusieurs stratégies pour le même utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="d5444-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="d5444-138">À chaque connexion, Azure Active Directory évalue toutes les stratégies et vérifie que toutes les conditions requises sont remplies avant d’accorder l’accès à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5444-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="d5444-139">L’accès conditionnel fonctionne-t-il avec Exchange ActiveSync ?</span><span class="sxs-lookup"><span data-stu-id="d5444-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="d5444-140">Oui, vous pouvez utiliser Exchange ActiveSync dans une stratégie d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="d5444-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="d5444-141">Ce que vous devez éviter</span><span class="sxs-lookup"><span data-stu-id="d5444-141">What you should avoid doing</span></span>

<span data-ttu-id="d5444-142">L’infrastructure d’accès conditionnel vous offre une souplesse de configuration exceptionnelle.</span><span class="sxs-lookup"><span data-stu-id="d5444-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="d5444-143">Toutefois, une grande souplesse signifie également que vous devez examiner chaque stratégie de configuration avant de la mettre en œuvre afin d’éviter des résultats indésirables.</span><span class="sxs-lookup"><span data-stu-id="d5444-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="d5444-144">Dans ce contexte, prêtez une attention particulière à l’affectation de jeux complets comme par exemple **tous les utilisateurs / groupes / applications cloud**.</span><span class="sxs-lookup"><span data-stu-id="d5444-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="d5444-145">Dans votre environnement, vous devez éviter les configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5444-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="d5444-146">**Pour tous les utilisateurs, toutes les applications cloud :**</span><span class="sxs-lookup"><span data-stu-id="d5444-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="d5444-147">**Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.</span><span class="sxs-lookup"><span data-stu-id="d5444-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="d5444-148">**Exiger un appareil conforme** : pour les utilisateurs qui n’ont pas encore inscrit leurs appareils, cette stratégie bloque tout accès, notamment l’accès au portail Intune.</span><span class="sxs-lookup"><span data-stu-id="d5444-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="d5444-149">Si vous êtes un administrateur sans appareil inscrit, cette stratégie vous bloque et vous ne pouvez pas retourner dans le portail Azure pour modifier la stratégie.</span><span class="sxs-lookup"><span data-stu-id="d5444-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="d5444-150">**Exiger la jonction de domaine** : ce blocage d’accès par stratégie peut également bloquer l’accès pour tous les utilisateurs de votre organisation si vous n’avez pas encore d’appareil joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="d5444-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="d5444-151">**Pour tous les utilisateurs, toutes les applications cloud, toutes les plates-formes d’appareils :**</span><span class="sxs-lookup"><span data-stu-id="d5444-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="d5444-152">**Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.</span><span class="sxs-lookup"><span data-stu-id="d5444-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="d5444-153">Scénarios courants</span><span class="sxs-lookup"><span data-stu-id="d5444-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="d5444-154">Exiger l’authentification multifacteur pour les applications</span><span class="sxs-lookup"><span data-stu-id="d5444-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="d5444-155">Dans de nombreux environnements, certaines applications nécessitent un niveau de protection plus élevé que d’autres.</span><span class="sxs-lookup"><span data-stu-id="d5444-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="d5444-156">C’est le cas des applications qui ont accès à des données sensibles.</span><span class="sxs-lookup"><span data-stu-id="d5444-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="d5444-157">Si vous souhaitez ajouter une couche de protection supplémentaire pour ces applications, vous pouvez configurer une stratégie d’accès conditionnel qui requiert l’authentification multifacteur lorsque les utilisateurs accèdent à ces applications.</span><span class="sxs-lookup"><span data-stu-id="d5444-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="d5444-158">Exiger l’authentification multifacteur pour l’accès à partir de réseaux non approuvés</span><span class="sxs-lookup"><span data-stu-id="d5444-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="d5444-159">Ce scénario est semblable au précédent, car il ajoute une exigence pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="d5444-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="d5444-160">Toutefois, la principale différence réside dans la condition de cette exigence.</span><span class="sxs-lookup"><span data-stu-id="d5444-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="d5444-161">Tandis que le scénario précédent se concentre sur les applications ayant accès à des données sensibles, ce scénario concerne les emplacements approuvés.</span><span class="sxs-lookup"><span data-stu-id="d5444-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="d5444-162">En d’autres termes, l’authentification multifacteur peut être requise si un utilisateur accède à une application à partir d’un réseau que vous n’avez pas approuvé.</span><span class="sxs-lookup"><span data-stu-id="d5444-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="d5444-163">Seuls les appareils approuvés ont accès aux services Office 365</span><span class="sxs-lookup"><span data-stu-id="d5444-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="d5444-164">Si vous utilisez Intune dans votre environnement, vous pouvez utiliser d’emblée l’interface de stratégie d’accès conditionnel dans la console Azure.</span><span class="sxs-lookup"><span data-stu-id="d5444-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="d5444-165">De nombreux clients Intune utilisent l’accès conditionnel pour vérifier que seuls les appareils approuvés ont accès aux services Office 365.</span><span class="sxs-lookup"><span data-stu-id="d5444-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="d5444-166">Cela signifie que les appareils mobiles sont inscrits dans Intune, qu’ils répondent aux critères de la stratégie de conformité et que des PC Windows sont joints à un domaine local.</span><span class="sxs-lookup"><span data-stu-id="d5444-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="d5444-167">L’avantage, c’est que vous n’avez pas à définir la même stratégie pour chacun des services Office 365.</span><span class="sxs-lookup"><span data-stu-id="d5444-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="d5444-168">Lorsque vous créez une stratégie, configurez les applications cloud pour inclure chacune des applications Office 365 que vous souhaitez protéger avec l’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="d5444-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5444-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d5444-169">Next steps</span></span>

<span data-ttu-id="d5444-170">Pour savoir comment configurer une stratégie d’accès conditionnel, consultez [Prise en main de l’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5444-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
