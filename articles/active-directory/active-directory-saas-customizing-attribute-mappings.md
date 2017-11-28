---
title: "aaaCustomizing des mappages d’attributs Active Directory de Azure | Documents Microsoft"
description: "Découvrez lesquels mappages d’attributs pour les applications SaaS dans Azure Active Directory sont comment vous pouvez modifier les tooaddress votre entreprise a besoin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="6de27-103">Personnalisation des mappages d’attributs d’approvisionnement d’utilisateurs pour les applications SaaS dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6de27-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="6de27-104">Microsoft Azure AD prend en charge les applications SaaS tierces toothird tels que Salesforce, Google Apps et d’autres de configuration de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6de27-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="6de27-105">Si vous disposez de configuration pour une application de SaaS tiers activée de l’utilisateur, hello portail de gestion Azure contrôle ses valeurs d’attribut dans le cadre d’une configuration appelée « mappage d’attribut ».</span><span class="sxs-lookup"><span data-stu-id="6de27-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="6de27-106">Il existe un ensemble préconfiguré de mappages d’attributs entre les objets utilisateur Azure AD et les objets utilisateur de chaque application SaaS.</span><span class="sxs-lookup"><span data-stu-id="6de27-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="6de27-107">Certaines applications gèrent d’autres types d’objets, tels que des groupes ou des contacts.</span><span class="sxs-lookup"><span data-stu-id="6de27-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="6de27-108">Vous pouvez personnaliser les mappages d’attributs par défaut hello selon les besoins de tooyour.</span><span class="sxs-lookup"><span data-stu-id="6de27-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="6de27-109">Cela signifie que vous pouvez modifier ou supprimer des mappages d’attributs existants ou en créer de nouveaux.</span><span class="sxs-lookup"><span data-stu-id="6de27-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="6de27-110">Dans le portail hello Azure AD, vous pouvez accéder à cette fonctionnalité en cliquant sur un **mappages** configuration sous **Provisioning** Bonjour **gérer** section d’un  **Application d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6de27-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="6de27-112">En cliquant sur un **mappages** configuration, ouvre hello liée **un mappage d’attribut** panneau.</span><span class="sxs-lookup"><span data-stu-id="6de27-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="6de27-113">Il existe des mappages d’attributs qui sont requis par une toofunction d’application SaaS correctement.</span><span class="sxs-lookup"><span data-stu-id="6de27-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="6de27-114">Pour les attributs requis, hello **supprimer** fonctionnalité n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="6de27-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="6de27-116">Dans l’exemple hello ci-dessus, vous pouvez voir que hello **nom d’utilisateur** attribut d’un objet géré dans Salesforce est rempli avec hello **userPrincipalName** valeur Hello liée objet Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6de27-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="6de27-117">Vous pouvez personnaliser des **mappages d’attributs** existants en cliquant sur un mappage.</span><span class="sxs-lookup"><span data-stu-id="6de27-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="6de27-118">Cette opération ouvre hello **modifier l’attribut** panneau.</span><span class="sxs-lookup"><span data-stu-id="6de27-118">This opens hello **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="6de27-120">Présentation des types de mappage d’attributs</span><span class="sxs-lookup"><span data-stu-id="6de27-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="6de27-121">Avec les mappages d’attributs, vous contrôlez la façon dont les attributs sont renseignés dans une application SaaS tierce.</span><span class="sxs-lookup"><span data-stu-id="6de27-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="6de27-122">Quatre différents types de mappages sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="6de27-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="6de27-123">**Direct** – attribut de hello cible est rempli avec la valeur hello d’un attribut de l’objet lié de hello dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6de27-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="6de27-124">**Constante** – attribut de cible de hello est rempli par une chaîne spécifique que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="6de27-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="6de27-125">**Expression** -attribut de hello cible est rempli en fonction de résultats d’une expression de type script hello.</span><span class="sxs-lookup"><span data-stu-id="6de27-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="6de27-126">Pour plus d’informations, consultez l’article [Écriture d’expressions pour les mappages d’attributs dans Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="6de27-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="6de27-127">**Aucun** -attribut cible de hello reste inchangée.</span><span class="sxs-lookup"><span data-stu-id="6de27-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="6de27-128">Toutefois, si l’attribut cible de hello est toujours vide, il est rempli avec la valeur par défaut hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="6de27-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="6de27-129">Dans types de mappage addition toothese quatre attributs de base, prend en charge les mappages d’attributs personnalisés concept hello de facultatif **par défaut** assignation de valeur.</span><span class="sxs-lookup"><span data-stu-id="6de27-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="6de27-130">assignation de la valeur par défaut Hello garantit qu’un attribut cible est rempli avec une valeur si elle existe aucune valeur dans Azure AD ou sur l’objet cible de hello.</span><span class="sxs-lookup"><span data-stu-id="6de27-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="6de27-131">configuration la plus courante Hello est tooleave ce vide.</span><span class="sxs-lookup"><span data-stu-id="6de27-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="6de27-132">Présentation des propriétés de mappage d’attributs</span><span class="sxs-lookup"><span data-stu-id="6de27-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="6de27-133">Dans la section précédente de hello, vous avez déjà été introduites toohello attribut mappage type propriété.</span><span class="sxs-lookup"><span data-stu-id="6de27-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="6de27-134">Dans la propriété toothis de plus, des mappages d’attributs prennent en charge également les hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="6de27-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="6de27-135">**Attribut source** -attribut utilisateur hello système source de hello (par exemple : Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6de27-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="6de27-136">**Attribut cible** : attribut d’utilisateur hello dans le système cible de hello (par exemple : ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="6de27-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="6de27-137">**Correspond à des objets à l’aide de cet attribut** : ce mappage doit être utilisé ou non toouniquely identifier les utilisateurs entre les systèmes source et cible hello.</span><span class="sxs-lookup"><span data-stu-id="6de27-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="6de27-138">Cela est généralement définie sur hello userPrincipalName ou attribut de messagerie dans Azure AD, qui est généralement mappé tooa des champs de nom d’utilisateur dans une application cible.</span><span class="sxs-lookup"><span data-stu-id="6de27-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="6de27-139">**Priorité des correspondances** : plusieurs attributs de correspondance peuvent être définis.</span><span class="sxs-lookup"><span data-stu-id="6de27-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="6de27-140">S’il existe plusieurs, ils sont évalués dans l’ordre de hello défini par ce champ.</span><span class="sxs-lookup"><span data-stu-id="6de27-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="6de27-141">Dès qu’une correspondance est trouvée, aucun autre attribut correspondant n’est évalué.</span><span class="sxs-lookup"><span data-stu-id="6de27-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="6de27-142">**Appliquer ce mappage**</span><span class="sxs-lookup"><span data-stu-id="6de27-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="6de27-143">**Toujours** : applique ce mappage à la création de l’utilisateur et des actions de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6de27-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="6de27-144">**Lors de la création uniquement** : applique ce mappage uniquement aux actions de création d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6de27-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="6de27-145">Ce que vous devez savoir</span><span class="sxs-lookup"><span data-stu-id="6de27-145">What you should know</span></span>

<span data-ttu-id="6de27-146">Microsoft Azure AD fournit une implémentation efficace d’un processus de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6de27-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="6de27-147">Dans un environnement initialisé, seuls les objets nécessitant des mises à jour sont traités pendant un cycle de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6de27-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="6de27-148">Mise à jour des mappages d’attributs d’a un impact sur les performances de hello d’un cycle de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6de27-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="6de27-149">Une configuration de mappage de mise à jour toohello attribut nécessite tous les objets managés toobe réévaluées.</span><span class="sxs-lookup"><span data-stu-id="6de27-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="6de27-150">Il est un meilleure pratique tookeep hello nombre de mappages d’attributs tooyour modifications consécutives au minimum.</span><span class="sxs-lookup"><span data-stu-id="6de27-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6de27-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6de27-151">Next steps</span></span>

* [<span data-ttu-id="6de27-152">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6de27-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6de27-153">Automatiser la configuration d’utilisateur/Deprovisioning tooSaaS applications</span><span class="sxs-lookup"><span data-stu-id="6de27-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="6de27-154">Écriture d’expressions pour les mappages d’attributs</span><span class="sxs-lookup"><span data-stu-id="6de27-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="6de27-155">Filtres d’étendue pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6de27-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="6de27-156">SCIM tooenable la configuration automatique des utilisateurs et groupes à partir d’Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="6de27-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="6de27-157">Notifications d’approvisionnement de comptes</span><span class="sxs-lookup"><span data-stu-id="6de27-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="6de27-158">Liste des didacticiels sur la façon de tooIntegrate applications SaaS</span><span class="sxs-lookup"><span data-stu-id="6de27-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

