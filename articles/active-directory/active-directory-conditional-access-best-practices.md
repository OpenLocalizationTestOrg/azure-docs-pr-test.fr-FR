---
title: "pratiques aaaBest pour l’accès conditionnel dans Azure Active Directory | Documents Microsoft"
description: "Découvrez-en davantage sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel."
services: active-directory
keywords: "tooapps d’accès conditionnel, l’accès conditionnel avec Azure AD, sécuriser l’accès aux ressources toocompany, les stratégies d’accès conditionnel"
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
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="c1f51-104">Meilleures pratiques l’accès conditionnel dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1f51-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="c1f51-105">Cette rubrique vous fournit des informations sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="c1f51-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="c1f51-106">Avant de lire cette rubrique, vous devez vous familiariser avec les concepts de hello et la terminologie de hello décrites dans [accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c1f51-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="c1f51-107">Ce que vous devez savoir</span><span class="sxs-lookup"><span data-stu-id="c1f51-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="c1f51-108">Les étapes nécessaires toomake un travail de la stratégie ?</span><span class="sxs-lookup"><span data-stu-id="c1f51-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="c1f51-109">Lorsque vous créez une stratégie, aucun utilisateur, groupe, application ou contrôle d’accès n’est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c1f51-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Applications cloud](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="c1f51-111">toomake votre stratégie fonctionne, vous devez configurer les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="c1f51-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="c1f51-112">Quoi</span><span class="sxs-lookup"><span data-stu-id="c1f51-112">What</span></span>           | <span data-ttu-id="c1f51-113">Comment</span><span class="sxs-lookup"><span data-stu-id="c1f51-113">How</span></span>                                  | <span data-ttu-id="c1f51-114">Pourquoi</span><span class="sxs-lookup"><span data-stu-id="c1f51-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="c1f51-115">**Applications cloud**</span><span class="sxs-lookup"><span data-stu-id="c1f51-115">**Cloud apps**</span></span> |<span data-ttu-id="c1f51-116">Vous devez tooselect une ou plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="c1f51-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="c1f51-117">Hello une stratégie d’accès conditionnel vise tooenable toofine ajuster comment les utilisateurs autorisés peuvent accéder à vos applications.</span><span class="sxs-lookup"><span data-stu-id="c1f51-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="c1f51-118">**Utilisateurs et groupes**</span><span class="sxs-lookup"><span data-stu-id="c1f51-118">**Users and groups**</span></span> | <span data-ttu-id="c1f51-119">Vous devez tooselect au moins un utilisateur ou un groupe qui est autorisé que vous avez sélectionné les applications cloud hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c1f51-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="c1f51-120">Une stratégie d’accès conditionnel, à laquelle aucun utilisateur ou groupe n’est affecté, n’est jamais déclenchée.</span><span class="sxs-lookup"><span data-stu-id="c1f51-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="c1f51-121">**Contrôles d’accès**</span><span class="sxs-lookup"><span data-stu-id="c1f51-121">**Access controls**</span></span> | <span data-ttu-id="c1f51-122">Vous devez tooselect au moins un contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="c1f51-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="c1f51-123">Votre stratégie processeur a besoin tooknow quel toodo si vos conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="c1f51-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="c1f51-124">En outre toothese conditions de base, dans de nombreux cas, vous devez également configurer une condition.</span><span class="sxs-lookup"><span data-stu-id="c1f51-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="c1f51-125">Une stratégie serait également fonctionner sans condition configurée, les conditions sont un facteur déterminant pour le paramétrage d’accès tooyour applications hello.</span><span class="sxs-lookup"><span data-stu-id="c1f51-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![Applications cloud](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="c1f51-127">Comment les affectations sont-elles évaluées ?</span><span class="sxs-lookup"><span data-stu-id="c1f51-127">How are assignments evaluated?</span></span>

<span data-ttu-id="c1f51-128">Toutes les attributions sont reliées par l’opérateur logique **AND**.</span><span class="sxs-lookup"><span data-stu-id="c1f51-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="c1f51-129">Si vous avez plusieurs attribution configurée, tootrigger une stratégie, toutes les attributions doivent être respectées.</span><span class="sxs-lookup"><span data-stu-id="c1f51-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="c1f51-130">Si vous devez tooconfigure une condition d’emplacement qui applique des connexions tooall sur en dehors du réseau de votre organisation, vous pouvez le faire par :</span><span class="sxs-lookup"><span data-stu-id="c1f51-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="c1f51-131">inclure **tous les emplacements**,</span><span class="sxs-lookup"><span data-stu-id="c1f51-131">Including **All locations**</span></span>
- <span data-ttu-id="c1f51-132">exclure **toutes les adresses IP approuvées**.</span><span class="sxs-lookup"><span data-stu-id="c1f51-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="c1f51-133">Que se passe-t-il si vous avez des stratégies dans hello portail Azure classic et le portail Azure configuré ?</span><span class="sxs-lookup"><span data-stu-id="c1f51-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="c1f51-134">Les deux stratégies sont appliquées par Azure Active Directory et hello utilisateur accès uniquement lorsque toutes les conditions requises sont remplies.</span><span class="sxs-lookup"><span data-stu-id="c1f51-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="c1f51-135">Que se passe-t-il si vous avez des stratégies dans hello portail Intune Silverlight et hello portail Azure ?</span><span class="sxs-lookup"><span data-stu-id="c1f51-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="c1f51-136">Les deux stratégies sont appliquées par Azure Active Directory et hello utilisateur accès uniquement lorsque toutes les conditions requises sont remplies.</span><span class="sxs-lookup"><span data-stu-id="c1f51-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="c1f51-137">Que se passe-t-il si j’ai plusieurs stratégies pour hello même utilisateur configuré ?</span><span class="sxs-lookup"><span data-stu-id="c1f51-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="c1f51-138">Pour chaque connexion, Azure Active Directory évalue toutes les stratégies et garantit que toutes les conditions requises sont remplies avant que l’utilisateur de toohello accès accordé.</span><span class="sxs-lookup"><span data-stu-id="c1f51-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="c1f51-139">L’accès conditionnel fonctionne-t-il avec Exchange ActiveSync ?</span><span class="sxs-lookup"><span data-stu-id="c1f51-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="c1f51-140">Oui, vous pouvez utiliser Exchange ActiveSync dans une stratégie d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="c1f51-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="c1f51-141">Ce que vous devez éviter</span><span class="sxs-lookup"><span data-stu-id="c1f51-141">What you should avoid doing</span></span>

<span data-ttu-id="c1f51-142">infrastructure d’accès conditionnel Hello vous offre une flexibilité de configuration excellent.</span><span class="sxs-lookup"><span data-stu-id="c1f51-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="c1f51-143">Toutefois, une grande souplesse signifie également que vous devez lire soigneusement chaque tooreleasing préalable de stratégie de configuration il tooavoid des résultats indésirables.</span><span class="sxs-lookup"><span data-stu-id="c1f51-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="c1f51-144">Dans ce contexte, vous devez prêter tooassignments une attention particulière affecter tels que les jeux complets **tous les utilisateurs / groupes / applications cloud**.</span><span class="sxs-lookup"><span data-stu-id="c1f51-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="c1f51-145">Dans votre environnement, vous devez éviter hello suivant configurations :</span><span class="sxs-lookup"><span data-stu-id="c1f51-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="c1f51-146">**Pour tous les utilisateurs, toutes les applications cloud :**</span><span class="sxs-lookup"><span data-stu-id="c1f51-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="c1f51-147">**Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.</span><span class="sxs-lookup"><span data-stu-id="c1f51-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="c1f51-148">**Exiger un appareil conforme** - pour les utilisateurs qui n’ont inscrit leurs appareils encore, cette stratégie bloque tout accès, y compris l’accès toohello Intune portail.</span><span class="sxs-lookup"><span data-stu-id="c1f51-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="c1f51-149">Si vous êtes un administrateur sans un appareil inscrit, cette stratégie bloque le retour à la stratégie de hello hello toochange portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f51-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="c1f51-150">**Exiger la jonction de domaine** - ce bloc de stratégie accès a également hello potentiels tooblock accès pour tous les utilisateurs de votre organisation si vous n’avez pas encore un appareil appartenant à un domaine.</span><span class="sxs-lookup"><span data-stu-id="c1f51-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="c1f51-151">**Pour tous les utilisateurs, toutes les applications cloud, toutes les plates-formes d’appareils :**</span><span class="sxs-lookup"><span data-stu-id="c1f51-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="c1f51-152">**Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.</span><span class="sxs-lookup"><span data-stu-id="c1f51-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="c1f51-153">Scénarios courants</span><span class="sxs-lookup"><span data-stu-id="c1f51-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="c1f51-154">Exiger l’authentification multifacteur pour les applications</span><span class="sxs-lookup"><span data-stu-id="c1f51-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="c1f51-155">De nombreux environnements disposent d’applications nécessitant un niveau de protection supérieur hello d’autres.</span><span class="sxs-lookup"><span data-stu-id="c1f51-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="c1f51-156">C’est, par exemple, les cas de hello pour les applications qui ont accès aux données de toosensitive.</span><span class="sxs-lookup"><span data-stu-id="c1f51-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="c1f51-157">Si vous souhaitez tooadd une autre couche de protection toothese applications, vous pouvez configurer une stratégie d’accès conditionnel qui requiert l’authentification multifacteur lorsque les utilisateurs accèdent à ces applications.</span><span class="sxs-lookup"><span data-stu-id="c1f51-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="c1f51-158">Exiger l’authentification multifacteur pour l’accès à partir de réseaux non approuvés</span><span class="sxs-lookup"><span data-stu-id="c1f51-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="c1f51-159">Ce scénario est le scénario précédent de toohello similaire, car elle ajoute la configuration requise pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="c1f51-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="c1f51-160">Toutefois, hello principale différence est condition hello pour cette spécification.</span><span class="sxs-lookup"><span data-stu-id="c1f51-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="c1f51-161">Lors de focus hello du scénario précédent de hello est sur les applications avec des données access toosensitve, hello ce scénario se concentre sur des emplacements approuvés.</span><span class="sxs-lookup"><span data-stu-id="c1f51-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="c1f51-162">En d’autres termes, l’authentification multifacteur peut être requise si un utilisateur accède à une application à partir d’un réseau que vous n’avez pas approuvé.</span><span class="sxs-lookup"><span data-stu-id="c1f51-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="c1f51-163">Seuls les appareils approuvés ont accès aux services Office 365</span><span class="sxs-lookup"><span data-stu-id="c1f51-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="c1f51-164">Si vous utilisez Intune dans votre environnement, vous pouvez commencer immédiatement à l’aide d’interface de stratégie d’accès conditionnel hello Bonjour console Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f51-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="c1f51-165">De nombreux clients Intune utilisent tooensure d’accès conditionnel qu’uniquement les appareils de confiance peuvent accéder aux services Office 365.</span><span class="sxs-lookup"><span data-stu-id="c1f51-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="c1f51-166">Cela signifie que les appareils mobiles sont inscrits avec Intune et répondre aux exigences de stratégie de conformité, et que les PC Windows appartiennent à un domaine local de tooan jointes.</span><span class="sxs-lookup"><span data-stu-id="c1f51-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="c1f51-167">Une amélioration importante est que vous n’avez pas tooset hello même stratégie pour chacun des services de hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="c1f51-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="c1f51-168">Lorsque vous créez une nouvelle stratégie, configurez hello Cloud applications tooinclude chaque des applications hello O365 que vous souhaitez tooprotect avec l’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="c1f51-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1f51-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1f51-169">Next steps</span></span>

<span data-ttu-id="c1f51-170">Si vous souhaitez tooknow tooconfigure une stratégie d’accès conditionnel, voir [prise en main avec un accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c1f51-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
