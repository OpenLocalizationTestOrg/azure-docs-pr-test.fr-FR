---
title: "Présentation du manuel de preuve de concept Azure Active Directory | Microsoft Docs"
description: "Explorer et implémenter rapidement des scénarios de gestion des identités et des accès"
services: active-directory
keywords: azure active directory, manuel, preuve de concept, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="e2ac8-104">Manuel de preuve de concept Azure Active Directory : Présentation</span><span class="sxs-lookup"><span data-stu-id="e2ac8-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="e2ac8-105">Cet article fournit des instructions pour explorer différentes fonctionnalités d’Azure AD dans une preuve de concept (PoC).</span><span class="sxs-lookup"><span data-stu-id="e2ac8-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="e2ac8-106">Le public concerné est celui des architectes d’identité, des professionnels de l’informatique et des intégrateurs de systèmes</span><span class="sxs-lookup"><span data-stu-id="e2ac8-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="e2ac8-107">Comment utiliser ce manuel</span><span class="sxs-lookup"><span data-stu-id="e2ac8-107">How to use this Playbook</span></span>

1. <span data-ttu-id="e2ac8-108">Utilisez la section [Thème](active-directory-playbook-ingredients.md#theme) pour choisir les domaines qui vous intéressent en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="e2ac8-109">Définissez l’étendue de cette preuve de concept en choisissant les scénarios correspondant aux objectifs de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="e2ac8-110">Plus le scénario est court, mieux c’est.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-110">The shorter the better.</span></span> <span data-ttu-id="e2ac8-111">Nous vous recommandons donc d’être aussi concis que possible pour transmettre la valeur aux parties prenantes tout en minimisant la complexité de la réalisation.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="e2ac8-112">Utilisez la section [Implémentation](active-directory-playbook-implementation.md) pour comprendre les différents scénarios et ce qu’ils signifient pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="e2ac8-113">Dans chaque scénario, nous décrivons comment le configurer (ce que nous appelons les [blocs de construction](active-directory-playbook-building-blocks.md)) et comment naviguer dans les scénarios.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="e2ac8-114">Chaque bloc de construction explique les conditions préalables requises, ainsi que le temps approximatif d’accomplissement.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="e2ac8-115">Cela peut vous aider pendant le processus de planification.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="e2ac8-116">Sur la base des points 1 à 3 ci-dessus, définissez l’[environnement](active-directory-playbook-ingredients.md#environment) d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="e2ac8-117">Nous vous encourageons à recourir à un environnement de production afin que vos utilisateurs aient une bonne perception de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="e2ac8-118">En cas d’exigences contradictoires, servez-vous de cette matrice de compromis très utile :</span><span class="sxs-lookup"><span data-stu-id="e2ac8-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="e2ac8-119">Démonstration de valeur centrée sur un thème</span><span class="sxs-lookup"><span data-stu-id="e2ac8-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="e2ac8-120">Fluidité de préparation, de configuration et d’exécution des scénarios</span><span class="sxs-lookup"><span data-stu-id="e2ac8-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="e2ac8-121">Minimum de temps pour l’exécution des scénarios cibles</span><span class="sxs-lookup"><span data-stu-id="e2ac8-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="e2ac8-122">Proximité maximale de la production compte tenu de vos contraintes</span><span class="sxs-lookup"><span data-stu-id="e2ac8-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="e2ac8-123">Cet article présente certains produits et applications tiers spécifiques mentionnés en temps qu’exemples pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="e2ac8-124">Azure AD prend en charge des milliers d’applications dans notre [Galerie d’applications](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps), que vous pouvez utiliser en fonction de vos besoins et de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e2ac8-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]