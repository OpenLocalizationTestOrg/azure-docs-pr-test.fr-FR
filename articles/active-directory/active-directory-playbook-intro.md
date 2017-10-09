---
title: "aaaAzure Active Directory preuve de concept manuel d’Introduction | Documents Microsoft"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="a307f-104">Manuel de preuve de concept Azure Active Directory : Présentation</span><span class="sxs-lookup"><span data-stu-id="a307f-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="a307f-105">Cet article fournit des instructions fonctionnalités tooexplore AD Azure différent dans une preuve de Concept (PoC).</span><span class="sxs-lookup"><span data-stu-id="a307f-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="a307f-106">Hello destinés à public de ce document est identité architectes, les professionnels de l’informatique et les intégrateurs système</span><span class="sxs-lookup"><span data-stu-id="a307f-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="a307f-107">Comment toouse ce manuel</span><span class="sxs-lookup"><span data-stu-id="a307f-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="a307f-108">Hello d’utilisation [thème](active-directory-playbook-ingredients.md#theme) section et choisir hello ou les zones d’intérêt en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="a307f-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="a307f-109">Définir l’étendue hello preuve de concept en choisissant les scénarios hello qui s’alignent sur vos objectifs professionnels.</span><span class="sxs-lookup"><span data-stu-id="a307f-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="a307f-110">Bonjour plus court Bonjour mieux.</span><span class="sxs-lookup"><span data-stu-id="a307f-110">hello shorter hello better.</span></span> <span data-ttu-id="a307f-111">Nous vous recommandons d’effectuer l’opération comme court et concis en tant que valeur de hello tooconvey possible les parties prenantes toohello tout en réduisant hello complexité toorealize il.</span><span class="sxs-lookup"><span data-stu-id="a307f-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="a307f-112">Hello d’utilisation [implémentation](active-directory-playbook-implementation.md) scénarios de section toounderstand hello et seraient leur signification pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a307f-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="a307f-113">Dans chaque scénario, nous décrivons comment tooset, configurez-le (ce que nous appelons [blocs de construction](active-directory-playbook-building-blocks.md)), et comment toonavigate hello scénarios.</span><span class="sxs-lookup"><span data-stu-id="a307f-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="a307f-114">Chaque bloc de construction explique hello préalables, ainsi que d’un toocomplete heure approximative.</span><span class="sxs-lookup"><span data-stu-id="a307f-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="a307f-115">Cela peut vous aider pendant le processus de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="a307f-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="a307f-116">En fonction de 1 à 3 ci-dessus, définir hello [environnement](active-directory-playbook-ingredients.md#environment) dans le tooexecute.</span><span class="sxs-lookup"><span data-stu-id="a307f-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="a307f-117">Nous vous invitons toostrive pour un tooget d’environnement de production une idée de l’expérience hello pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a307f-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="a307f-118">En cas d’exigences contradictoires, servez-vous de cette matrice de compromis très utile :</span><span class="sxs-lookup"><span data-stu-id="a307f-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="a307f-119">Démonstration de valeur centrée sur un thème</span><span class="sxs-lookup"><span data-stu-id="a307f-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="a307f-120">Scénarios de hello tooprepare et tooset des tooexecute de lissage</span><span class="sxs-lookup"><span data-stu-id="a307f-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="a307f-121">Scénarios cibles de temps minimal tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="a307f-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="a307f-122">En tant que tooproduction ferme en tant que possible au sein de vos contraintes</span><span class="sxs-lookup"><span data-stu-id="a307f-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="a307f-123">Cet article présente certains produits et applications tiers spécifiques mentionnés en temps qu’exemples pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="a307f-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="a307f-124">Azure AD prend en charge des milliers d’applications dans notre [Galerie d’applications](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps), que vous pouvez utiliser en fonction de vos besoins et de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a307f-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]