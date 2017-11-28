---
title: "aaaAzure identité hybride de Active Directory des considérations de conception : déterminer les tâches de gestion des identités hybrides | Documents Microsoft"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello que vous choisissez lors de l’authentification utilisateur de hello et avant d’autoriser l’accès toohello application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a><span data-ttu-id="ebb1f-104">Planifier le cycle de vie des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="ebb1f-104">Plan for Hybrid Identity Lifecycle</span></span>
<span data-ttu-id="ebb1f-105">Identité est un des fondements de hello de votre stratégie d’accès enterprise mobility et d’application.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-105">Identity is one of hello foundations of your enterprise mobility and application access strategy.</span></span> <span data-ttu-id="ebb1f-106">Si vous vous connectez sur les appareils mobiles tooyour ou application SaaS, votre identité est hello toogaining clé accès tooeverything.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-106">Whether you are signing on tooyour mobile device or SaaS app, your identity is hello key toogaining access tooeverything.</span></span> <span data-ttu-id="ebb1f-107">À son niveau le plus élevé, une solution de gestion des identités englobe unifier et la synchronisation entre vos espaces de stockage qui inclut l’automatisation et la centralisation des processus hello de provisionnement des ressources.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-107">At its highest level, an identity management solution encompasses unifying and syncing between your identity repositories which includes automating and centralizing hello process of provisioning resources.</span></span> <span data-ttu-id="ebb1f-108">solution d’identité Hello doit être une identité centralisée entre locaux et cloud également utiliser une forme d’une authentification centralisée identity federation toomaintain et en toute sécurité et de partager avec les entreprises et les utilisateurs externes.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-108">hello identity solution should be a centralized identity across on-premises and cloud and also use some form of identity federation toomaintain centralized authentication and securely share and collaborate with external users and businesses.</span></span> <span data-ttu-id="ebb1f-109">Plage de ressources à partir des systèmes d’exploitation et applications toopeople ou sont associée à une organisation.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-109">Resources range from operating systems and applications toopeople in, or affiliated with, an organization.</span></span> <span data-ttu-id="ebb1f-110">Structure d’organisation peut être modifiée tooaccommodate stratégies de configuration hello et les procédures.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-110">Organizational structure can be altered tooaccommodate hello provisioning policies and procedures.</span></span>

<span data-ttu-id="ebb1f-111">Il est également important de toohave une solution d’identité axées tooempower vos utilisateurs en leur fournissant des expériences de libre-service tookeep leur productivité.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-111">It is also important toohave an identity solution geared tooempower your users by providing them with self-service experiences tookeep them productive.</span></span> <span data-ttu-id="ebb1f-112">Votre solution d’identité est plus robuste, si elle permet l’authentification unique pour les utilisateurs sur toutes les ressources hello que dont ils ont besoin d’accéder aux administrateurs tout niveaux peuvent utiliser les procédures standard pour la gestion des informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-112">Your identity solution is more robust if it enables single sign-on for users across all hello resources they need access Administrators at all levels can use standardized procedures for managing user credentials.</span></span> <span data-ttu-id="ebb1f-113">Certains niveaux d’administration peut être réduit ou éliminé, en fonction de l’ampleur hello Hello solution de gestion de configuration.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-113">Some levels of administration can be reduced or eliminated, depending on hello breadth of hello provisioning management solution.</span></span> <span data-ttu-id="ebb1f-114">En outre, vous pouvez en toute sécurité distribuer les capacités d'administration, manuellement ou automatiquement, entre différentes organisations.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-114">Furthermore, you can securely distribute administration capabilities, manually or automatically, among various organizations.</span></span> <span data-ttu-id="ebb1f-115">Par exemple, un administrateur de domaine peut traiter uniquement des personnes de hello et des ressources de ce domaine.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-115">For example, a domain administrator can serve only hello people and resources in that domain.</span></span> <span data-ttu-id="ebb1f-116">Cet utilisateur peut exécuter des tâches d’administration et de configuration, mais est toodo non autorisé des tâches de configuration, telles que la création de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-116">This user can do administrative and provisioning tasks, but is not authorized toodo configuration tasks, such as creating workflows.</span></span>

## <a name="determine-hybrid-identity-management-tasks"></a><span data-ttu-id="ebb1f-117">Déterminer les tâches de gestion des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="ebb1f-117">Determine Hybrid Identity Management Tasks</span></span>
<span data-ttu-id="ebb1f-118">Distribuer des tâches d’administration dans votre organisation améliore la précision de hello et l’efficacité de l’administration et améliore le solde hello de charge de travail hello d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-118">Distributing administrative tasks in your organization improves hello accuracy and effectiveness of administration and improves hello balance of hello workload of an organization.</span></span> <span data-ttu-id="ebb1f-119">Voici les tableaux croisés dynamiques hello qui définissent un système de gestion d’identité fiable.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-119">Following are hello pivots that define a robust identity management system.</span></span>

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

<span data-ttu-id="ebb1f-120">toodefine tâches de gestion d’identité hybride, vous devez comprendre certaines caractéristiques essentielles d’une organisation hello qui va être adopté identité hybride.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-120">toodefine hybrid identity management tasks, you must understand some essential characteristics of hello organization that will be adopting hybrid identity.</span></span> <span data-ttu-id="ebb1f-121">Il est utilisés pour les sources de l’identité des référentiels actuelle hello toounderstand important.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-121">It is important toounderstand hello current repositories being used for identity sources.</span></span> <span data-ttu-id="ebb1f-122">Connaître les éléments de base, vous aurez besoins fondamentaux de hello et selon que vous devez tooask plus granulaire aux questions qui vous guideront tooa meilleure décision de conception de votre solution d’identité.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-122">By knowing those core elements, you will have hello foundational requirements and based on that you will need tooask more granular questions that will lead you tooa better design decision for your Identity solution.</span></span>  

<span data-ttu-id="ebb1f-123">Lorsque vous définissez ces exigences, vérifiez que hello au moins suivant questions sont traitées.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-123">While defining those requirements, ensure that at least hello following questions are answered</span></span>

* <span data-ttu-id="ebb1f-124">Options d’approvisionnement :</span><span class="sxs-lookup"><span data-stu-id="ebb1f-124">Provisioning options:</span></span> 
  
  * <span data-ttu-id="ebb1f-125">Solution d’identité hybride hello prend-il en charge un système de configuration et de gestion de l’accès robuste ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-125">Does hello hybrid identity solution support a robust account access management and provisioning system?</span></span>
  * <span data-ttu-id="ebb1f-126">Comment sont des utilisateurs, groupes et les mots de passe va toobe géré ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-126">How are users, groups, and passwords going toobe managed?</span></span>
  * <span data-ttu-id="ebb1f-127">Gestion du cycle de vie des identités hello est-elle réactive</span><span class="sxs-lookup"><span data-stu-id="ebb1f-127">Is hello identity lifecycle management responsive?</span></span> 
    * <span data-ttu-id="ebb1f-128">Combien de temps prend la suspension du compte de mises à jour du mot de passe ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-128">How long does password updates account suspension take?</span></span>
* <span data-ttu-id="ebb1f-129">Gestion des licences :</span><span class="sxs-lookup"><span data-stu-id="ebb1f-129">License management:</span></span> 
  
  * <span data-ttu-id="ebb1f-130">Hello gestion des licences handles hybride identité solution ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-130">Does hello hybrid identity solution handles license management?</span></span>
    * <span data-ttu-id="ebb1f-131">Si oui, quelles sont les fonctionnalités disponibles ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-131">If yes, what capabilities are available?</span></span>
* <span data-ttu-id="ebb1f-132">Hello solution basée sur le groupe de licences gérer ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-132">Does hello solution handle group-based license management?</span></span> 
  
      - <span data-ttu-id="ebb1f-133">Si Oui, il est possible de tooassign un tooit de groupe de sécurité ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-133">If yes, is it possible tooassign a security group tooit?</span></span> 
       - <span data-ttu-id="ebb1f-134">Si Oui, annuaire de cloud hello attribue automatiquement des licences tooall des membres de hello du groupe de hello ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-134">If yes, will hello cloud directory automatically assign licenses tooall hello members of hello group?</span></span> 
        - <span data-ttu-id="ebb1f-135">Que se passe-t-il si un utilisateur est ensuite ajouté ou supprimé du groupe de hello, sera une licence automatiquement attribuée ou supprimée le cas échéant ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-135">What happens if a user is subsequently added to, or removed from hello group, will a license be automatically assigned or removed as appropriate?</span></span> 
* <span data-ttu-id="ebb1f-136">Intégration avec des fournisseurs d'identité tiers :</span><span class="sxs-lookup"><span data-stu-id="ebb1f-136">Integration with other third-party identity providers:</span></span>
* <span data-ttu-id="ebb1f-137">Cette solution hybride peut être intégrée avec identité tiers fournisseurs tooimplement l’authentification unique ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-137">Can this hybrid solution be integrated with third-party identity providers tooimplement single sign-on?</span></span>
* <span data-ttu-id="ebb1f-138">Il est possible de toounify tous hello différents fournisseurs d’identité dans un système d’identité cohérente ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-138">Is it possible toounify all hello different identity providers into a cohesive identity system?</span></span>
* <span data-ttu-id="ebb1f-139">Si oui, comment, qui sont-ils et quelles fonctionnalités sont disponibles ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-139">If yes, how and which are they and what capabilities are available?</span></span>

## <a name="synchronization-management"></a><span data-ttu-id="ebb1f-140">Gestion de la synchronisation</span><span class="sxs-lookup"><span data-stu-id="ebb1f-140">Synchronization Management</span></span>
<span data-ttu-id="ebb1f-141">Un des objectifs de hello d’un gestionnaire d’identité, toobring en mesure de toobe tous hello fournisseurs d’identité et les garder synchronisés.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-141">One of hello goals of an identity manager, toobe able toobring all hello identity providers and keep them synchronized.</span></span> <span data-ttu-id="ebb1f-142">Vous conservez les données hello synchronisées basée sur un fournisseur d’identité maître faisant autorité.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-142">You keep hello data synchronized based on an authoritative master identity provider.</span></span> <span data-ttu-id="ebb1f-143">Dans un scénario d’identité hybride, avec un modèle d’administration synchronisés, vous gérez toutes les identités d’utilisateur et appareil dans un serveur local et synchronisez les comptes hello et, éventuellement, cloud toohello de mots de passe.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-143">In a hybrid identity scenario, with a synchronized management model, you manage all user and device identities in an on-premises server and synchronize hello accounts and, optionally, passwords toohello cloud.</span></span> <span data-ttu-id="ebb1f-144">utilisateur de Hello entre des hello même mot de passe local comme il le fait dans le cloud de hello et à la connexion, hello mot de passe est vérifié par une solution d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-144">hello user enters hello same password on-premises as he or she does in hello cloud, and at sign-in, hello password is verified by hello identity solution.</span></span> <span data-ttu-id="ebb1f-145">Ce modèle utilise un outil de synchronisation d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="ebb1f-145">This model uses a directory synchronization tool.</span></span>

<span data-ttu-id="ebb1f-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png)synchronisation de hello tooproper conception de votre solution d’identité hybride vous assurer que hello suivant questions sont traités : • quelles sont les solutions de synchronisation hello disponibles pour la solution d’identité hybride hello ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png) tooproper design hello synchronization of your hybrid identity solution ensure that hello following questions are answered: •    What are hello sync solutions available for hello hybrid identity solution?</span></span>
<span data-ttu-id="ebb1f-147">• Quels sont l’authentification unique hello fonctionnalités disponibles ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-147">•    What are hello single sign on capabilities available?</span></span>
<span data-ttu-id="ebb1f-148">• Quelles sont les options de hello pour la fédération des identités entre B2B et B2C ?</span><span class="sxs-lookup"><span data-stu-id="ebb1f-148">•    What are hello options for identity federation between B2B and B2C?</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebb1f-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebb1f-149">Next steps</span></span>
[<span data-ttu-id="ebb1f-150">Déterminer la stratégie d’adoption de la gestion des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="ebb1f-150">Determine hybrid identity management adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="ebb1f-151">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ebb1f-151">See Also</span></span>
[<span data-ttu-id="ebb1f-152">Présentation des considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="ebb1f-152">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)
