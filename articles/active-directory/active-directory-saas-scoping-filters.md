---
title: "Approvisionnement d’applications avec filtres d’étendue | Microsoft Docs"
description: "Découvrez comment utiliser des filtres d’étendue pour empêcher les objets dans les applications qui prennent en charge l’approvisionnement automatisé des utilisateurs d’être approvisionnés si un objet n’est pas conforme à vos besoins."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="70a60-103">Approvisionnement d’applications basé sur les attributs avec filtres d’étendue</span><span class="sxs-lookup"><span data-stu-id="70a60-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="70a60-104">L’objectif de cette section est d’expliquer comment utiliser des filtres d’étendue pour définir des règles basées sur des attributs qui déterminent quels utilisateurs sont approvisionnés pour l’application.</span><span class="sxs-lookup"><span data-stu-id="70a60-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="70a60-105">Clauses et groupes d’étendue</span><span class="sxs-lookup"><span data-stu-id="70a60-105">Clauses and Scope Groups</span></span>
![Filtre d’étendue][1] 

<span data-ttu-id="70a60-107">Les filtres d’étendue sont définis par un ou plusieurs **groupes d’étendue**, chacun contenant une ou plusieurs **clauses**.</span><span class="sxs-lookup"><span data-stu-id="70a60-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="70a60-108">Pour afficher les clauses d’un groupe d’étendue particulier, développez-le en cliquant sur la flèche située à gauche du nom du groupe.</span><span class="sxs-lookup"><span data-stu-id="70a60-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="70a60-109">Une **clause** détermine quels utilisateurs sont autorisés à traverser le filtre d’étendue en évaluant les attributs de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="70a60-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="70a60-110">Par exemple, l’une de vos clauses peut exiger que l’attribut « état » d’un utilisateur soit égal à New York, afin que seuls les utilisateurs de New York soient approvisionnés dans l’application.</span><span class="sxs-lookup"><span data-stu-id="70a60-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Nom du groupe d’étendue][2] 

<span data-ttu-id="70a60-112">Chaque **groupe d’étendue** commence par une **clause** obligatoire, comme illustré dans la capture d’écran ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="70a60-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="70a60-113">Cette clause stipule simplement que l’utilisateur doit être préalablement affecté à l’application avant son évaluation par vos filtres d’étendue.</span><span class="sxs-lookup"><span data-stu-id="70a60-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="70a60-114">Cette clause ne peut pas être supprimée ou modifiée.</span><span class="sxs-lookup"><span data-stu-id="70a60-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="70a60-115">Vous pouvez ajouter de nouvelles clauses ou de nouveaux groupes d’étendue en appuyant sur le bouton approprié.</span><span class="sxs-lookup"><span data-stu-id="70a60-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="70a60-116">Vous pouvez attribuer un nom à chaque groupe d’étendue en modifiant sa propriété **Nom du groupe d’étendue** .</span><span class="sxs-lookup"><span data-stu-id="70a60-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="70a60-117">Évaluation des filtres d’étendue</span><span class="sxs-lookup"><span data-stu-id="70a60-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="70a60-118">Lors de l’approvisionnement, nous testons chaque utilisateur affecté par rapport à vos filtres d’étendue pour déterminer si cet utilisateur mérite l’accès à l’application.</span><span class="sxs-lookup"><span data-stu-id="70a60-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="70a60-119">On peut considérer chaque clause comme un test qui doit être réussi pour que l’utilisateur ne soit pas filtré et exclu.</span><span class="sxs-lookup"><span data-stu-id="70a60-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="70a60-120">Si vous avez défini plusieurs groupes d’étendue, chaque utilisateur doit satisfaire à au moins l’un d’eux pour accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="70a60-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="70a60-121">Dans chaque groupe d’étendue, toutefois, l’utilisateur doit satisfaire à chaque clause pour satisfaire à ce groupe d’étendue spécifique.</span><span class="sxs-lookup"><span data-stu-id="70a60-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="70a60-122">En d’autres termes, on peut considérer les groupes d’étendue comme étant liés par une opération logique OU et les clauses au sein de ces groupes comme étant liées par une opération logique ET.</span><span class="sxs-lookup"><span data-stu-id="70a60-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="70a60-123">Par exemple, considérez le filtre d’étendue ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="70a60-123">For example, consider the scoping filter below:</span></span>

![Nom du groupe d’étendue][3]  

<span data-ttu-id="70a60-125">D’après ce filtre d’étendue, les utilisateurs doivent satisfaire aux critères suivants pour être approvisionnés :</span><span class="sxs-lookup"><span data-stu-id="70a60-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="70a60-126">Ils doivent être affectés à l’application.</span><span class="sxs-lookup"><span data-stu-id="70a60-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="70a60-127">Ils doivent travailler dans le service Ingénierie</span><span class="sxs-lookup"><span data-stu-id="70a60-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="70a60-128">Ils doivent travailler à San Francisco ou au Canada.</span><span class="sxs-lookup"><span data-stu-id="70a60-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="70a60-129">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="70a60-129">Related Articles</span></span>
* [<span data-ttu-id="70a60-130">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70a60-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="70a60-131">Automatisation de l’approvisionnement et de l’annulation de l’approvisionnement des utilisateurs pour les applications SaaS</span><span class="sxs-lookup"><span data-stu-id="70a60-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="70a60-132">Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="70a60-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="70a60-133">Écriture d’expressions pour les mappages d’attributs</span><span class="sxs-lookup"><span data-stu-id="70a60-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="70a60-134">Notifications d’approvisionnement de comptes</span><span class="sxs-lookup"><span data-stu-id="70a60-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="70a60-135">Utilisation de SCIM pour activer la configuration automatique des utilisateurs et des groupes d’Azure Active Directory sur des applications</span><span class="sxs-lookup"><span data-stu-id="70a60-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="70a60-136">Liste des didacticiels sur l’intégration des applications SaaS</span><span class="sxs-lookup"><span data-stu-id="70a60-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
