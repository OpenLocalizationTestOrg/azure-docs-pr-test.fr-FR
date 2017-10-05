---
title: "Azure Active Directory B2C : Notes du développeur sur l’utilisation des stratégies personnalisées | Microsoft Docs"
description: "Notes à destination des développeurs pour configurer et maintenir Azure AD B2C avec des stratégies personnalisées"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="9947f-103">Notes de version pour la version préliminaire publique de la stratégie personnalisée Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="9947f-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="9947f-104">L’ensemble de fonctionnalités de stratégie personnalisée est désormais disponible à des fins d’évaluation en préversion publique pour tous les clients Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="9947f-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="9947f-105">Cet ensemble de fonctionnalités est destiné aux développeurs d’identité avancés créant les solutions d’identité les plus complexes.</span><span class="sxs-lookup"><span data-stu-id="9947f-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="9947f-106">À ce jour, cet ensemble de fonctionnalités exige que les développeurs configurent l’infrastructure d’expérience d’identité directement via la modification du fichier XML.</span><span class="sxs-lookup"><span data-stu-id="9947f-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="9947f-107">Cette méthode de configuration est à la fois puissante et complexe.</span><span class="sxs-lookup"><span data-stu-id="9947f-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="9947f-108">Les développeurs d’identité avancés qui utilisent l’infrastructure d’expérience d’identité doivent prévoir du temps pour suivre des procédures et lire des documents de référence.</span><span class="sxs-lookup"><span data-stu-id="9947f-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="9947f-109">Fonctionnalités incluses dans cette version préliminaire publique</span><span class="sxs-lookup"><span data-stu-id="9947f-109">Features included in this public preview</span></span>
<span data-ttu-id="9947f-110">Les nouvelles fonctionnalités introduites dans la préversion permettent aux développeurs d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="9947f-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="9947f-111">Créer et charger des parcours utilisateur d’authentification personnalisés à l’aide de stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9947f-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="9947f-112">Décrire des parcours utilisateur étape par étape comme des échanges entre des fournisseurs de revendications.</span><span class="sxs-lookup"><span data-stu-id="9947f-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="9947f-113">Définir le branchement conditionnel dans des parcours utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9947f-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="9947f-114">Intégrer des services compatibles avec l’API REST dans vos parcours utilisateur d’authentification personnalisés.</span><span class="sxs-lookup"><span data-stu-id="9947f-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="9947f-115">Ajouter la fédération avec les fournisseurs d’identité conformes à la norme OpenIDConnect.</span><span class="sxs-lookup"><span data-stu-id="9947f-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="9947f-116">Ajouter la fédération avec les fournisseurs d’identité qui adhèrent au protocole SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="9947f-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="9947f-117">Conditions de la version préliminaire publique</span><span class="sxs-lookup"><span data-stu-id="9947f-117">Terms of the public preview</span></span>

* <span data-ttu-id="9947f-118">Nous vous encourageons à utiliser les nouvelles fonctionnalités à des fins d’évaluation uniquement.</span><span class="sxs-lookup"><span data-stu-id="9947f-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="9947f-119">Les nouvelles fonctionnalités ne sont pas destinées à une utilisation dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9947f-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="9947f-120">Les contrats de niveau de service (SLA) ne s’appliquent pas aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="9947f-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="9947f-121">Les demandes de support peuvent être déposées via les canaux de support habituels.</span><span class="sxs-lookup"><span data-stu-id="9947f-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="9947f-122">Il n’existe aucune date prévue pour une mise à disposition générale.</span><span class="sxs-lookup"><span data-stu-id="9947f-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="9947f-123">À notre discrétion et pour quelque raison que ce soit, Microsoft peut signaler et rejeter ou limiter des scénarios et des parcours utilisateur qui dépassent la portée de la charte du produit Azure AD B2C comme plateforme de gestion des accès et des identités des clients.</span><span class="sxs-lookup"><span data-stu-id="9947f-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="9947f-124">Responsabilités des développeurs de l’ensemble de fonctionnalités de stratégie personnalisée</span><span class="sxs-lookup"><span data-stu-id="9947f-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="9947f-125">La configuration de stratégie manuelle accorde le niveau d’accès minimal à la plateforme sous-jacente d’Azure AD B2C et entraîne la création d’une infrastructure approuvée unique et entièrement personnalisable.</span><span class="sxs-lookup"><span data-stu-id="9947f-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="9947f-126">Les permutations possibles des fournisseurs d’identité personnalisés, les relations d’approbation, les intégrations aux services externes et les flux de travail étape par étape exigeront beaucoup de la part des développeurs avancés qui les utilisent.</span><span class="sxs-lookup"><span data-stu-id="9947f-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="9947f-127">Afin de tirer pleinement parti de la préversion publique, nous suggérons aux développeurs qui utilisent l’ensemble de fonctionnalités de stratégie personnalisée de respecter les consignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9947f-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="9947f-128">Se familiariser au langage de configuration du moteur d’expérience d’identité et à la gestion clé/secrets.</span><span class="sxs-lookup"><span data-stu-id="9947f-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="9947f-129">S’approprier les scénarios et les intégrations personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9947f-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="9947f-130">Effectuer un test de scénario méthodique.</span><span class="sxs-lookup"><span data-stu-id="9947f-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="9947f-131">Suivre les meilleures pratiques de test et de développement de logiciels avec au minimum un environnement de développement et de test et un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9947f-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="9947f-132">Suivre les nouveaux développements des services et fournisseurs d’identité que vous intégrez.</span><span class="sxs-lookup"><span data-stu-id="9947f-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="9947f-133">Par exemple, suivre les modifications apportées aux secrets, ainsi que les modifications planifiées et non planifiées du service.</span><span class="sxs-lookup"><span data-stu-id="9947f-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="9947f-134">Configurer la surveillance active et surveiller la réactivité des environnements de production.</span><span class="sxs-lookup"><span data-stu-id="9947f-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="9947f-135">Garder les adresses e-mail de contact à jour et rester attentif aux e-mails de l’équipe de site en ligne Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9947f-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="9947f-136">Prendre les mesures adéquates lorsque cela est recommandé par l’équipe de site en ligne Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9947f-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="9947f-137">Ces fonctionnalités peuvent éventuellement être incluses à des stratégies intégrées Azure AD, ce qui les rend plus accessibles à tous les développeurs.</span><span class="sxs-lookup"><span data-stu-id="9947f-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9947f-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9947f-138">Next steps</span></span>
<span data-ttu-id="9947f-139">[Azure Active Directory B2C : bien démarrer avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9947f-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
