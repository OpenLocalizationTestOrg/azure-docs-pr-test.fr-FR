---
title: "applications aaaProvisioning avec des filtres d’étendue | Documents Microsoft"
description: "Découvrez comment toouse étendue filtre les objets tooprevent dans les applications qui prennent en charge l’approvisionnement automatique des utilisateurs d’être réellement configuré si un objet n’est pas conforme à vos besoins."
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
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="dcec9-103">Approvisionnement d’applications basé sur les attributs avec filtres d’étendue</span><span class="sxs-lookup"><span data-stu-id="dcec9-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="dcec9-104">objectif Hello de cette section est tooexplain toouse étendue comment les filtres toodefine basée sur les attributs des règles qui déterminent quels utilisateurs sont mis en service toohello application.</span><span class="sxs-lookup"><span data-stu-id="dcec9-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="dcec9-105">Clauses et groupes d’étendue</span><span class="sxs-lookup"><span data-stu-id="dcec9-105">Clauses and Scope Groups</span></span>
![Filtre d’étendue][1] 

<span data-ttu-id="dcec9-107">Les filtres d’étendue sont définis par un ou plusieurs **groupes d’étendue**, chacun contenant une ou plusieurs **clauses**.</span><span class="sxs-lookup"><span data-stu-id="dcec9-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="dcec9-108">clauses de hello toosee pour un groupe d’étendue particulier, développez-le en cliquant sur hello flèche toohello gauche du nom du groupe hello.</span><span class="sxs-lookup"><span data-stu-id="dcec9-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="dcec9-109">A **clause** détermine quels utilisateurs sont autorisés à toopass via hello filtre d’étendue en évaluant les attributs de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dcec9-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="dcec9-110">Par exemple, vous pouvez avoir une clause qui impose que « état » attribut égal New York l’utilisateur, donc seuls les utilisateurs de New York sont configurés dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="dcec9-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![Nom du groupe d’étendue][2] 

<span data-ttu-id="dcec9-112">Chaque **groupe d’étendue** commence par un obligatoire **clause**, comme illustré dans la capture d’écran hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="dcec9-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="dcec9-113">Cette clause déclare simplement que l’utilisateur hello doit d’abord être affecté toohello application avant son évaluation par vos filtres d’étendue.</span><span class="sxs-lookup"><span data-stu-id="dcec9-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="dcec9-114">Cette clause ne peut pas être supprimée ou modifiée.</span><span class="sxs-lookup"><span data-stu-id="dcec9-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="dcec9-115">Vous pouvez ajouter de nouvelles clauses ou nouveaux groupes d’étendue en appuyant sur le bouton approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="dcec9-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="dcec9-116">Vous pouvez attribuer un nom à chaque groupe d’étendue en modifiant sa propriété **Nom du groupe d’étendue** .</span><span class="sxs-lookup"><span data-stu-id="dcec9-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="dcec9-117">Évaluation des filtres d’étendue</span><span class="sxs-lookup"><span data-stu-id="dcec9-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="dcec9-118">Lors de la configuration, nous testons chaque utilisateur affecté par rapport à votre portée toodetermine de filtres si cet utilisateur mérite accès toohello application.</span><span class="sxs-lookup"><span data-stu-id="dcec9-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="dcec9-119">Vous pouvez considérer chaque clause comme un test qui doive être passé dans l’ordre pour hello utilisateur tooavoid est rejeté.</span><span class="sxs-lookup"><span data-stu-id="dcec9-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="dcec9-120">Si vous avez plusieurs groupes d’étendue définies, chaque utilisateur doit au moins un d'entre eux tooaccess passer application hello.</span><span class="sxs-lookup"><span data-stu-id="dcec9-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="dcec9-121">Au sein de chaque groupe d’étendue, toutefois, hello utilisateur doit passer chaque toopass clause ce groupe d’étendue spécifique.</span><span class="sxs-lookup"><span data-stu-id="dcec9-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="dcec9-122">En d’autres termes, vous pouvez considérer les groupes d’étendue comme étant ou liés, et vous pouvez considérer clauses hello comme en cours et liés.</span><span class="sxs-lookup"><span data-stu-id="dcec9-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="dcec9-123">Par exemple, considérez hello ci-dessous de filtre d’étendue :</span><span class="sxs-lookup"><span data-stu-id="dcec9-123">For example, consider hello scoping filter below:</span></span>

![Nom du groupe d’étendue][3]  

<span data-ttu-id="dcec9-125">En fonction de filtre d’étendue de toothis, les utilisateurs doivent satisfaire suivant de hello critères, toobe configuré :</span><span class="sxs-lookup"><span data-stu-id="dcec9-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="dcec9-126">Ils doivent avoir toohello application.</span><span class="sxs-lookup"><span data-stu-id="dcec9-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="dcec9-127">Ils doivent travailler dans le service d’ingénierie hello</span><span class="sxs-lookup"><span data-stu-id="dcec9-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="dcec9-128">Ils doivent travailler à San Francisco ou au Canada.</span><span class="sxs-lookup"><span data-stu-id="dcec9-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="dcec9-129">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="dcec9-129">Related Articles</span></span>
* [<span data-ttu-id="dcec9-130">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcec9-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="dcec9-131">Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications</span><span class="sxs-lookup"><span data-stu-id="dcec9-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="dcec9-132">Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="dcec9-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="dcec9-133">Écriture d’expressions pour les mappages d’attributs</span><span class="sxs-lookup"><span data-stu-id="dcec9-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="dcec9-134">Notifications d’approvisionnement de comptes</span><span class="sxs-lookup"><span data-stu-id="dcec9-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="dcec9-135">SCIM tooenable la configuration automatique des utilisateurs et groupes à partir d’Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="dcec9-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="dcec9-136">Liste des didacticiels sur la façon de tooIntegrate applications SaaS</span><span class="sxs-lookup"><span data-stu-id="dcec9-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
