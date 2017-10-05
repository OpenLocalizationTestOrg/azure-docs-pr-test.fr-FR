---
title: "Ingrédients du manuel de PoC Azure Active Directory | Microsoft Docs"
description: "Explorer et implémenter rapidement des scénarios de gestion de l'identité et de l'accès"
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
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="49070-104">Ingrédients du manuel de preuve de concept Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49070-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="49070-105">Thème</span><span class="sxs-lookup"><span data-stu-id="49070-105">Theme</span></span>
<span data-ttu-id="49070-106">Azure AD fournit des solutions d’identité et des accès dans plusieurs domaines de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="49070-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="49070-107">Nous classons les scénarios dans les domaines suivants :</span><span class="sxs-lookup"><span data-stu-id="49070-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="49070-108">Un grand nombre d’applications, une seule identité</span><span class="sxs-lookup"><span data-stu-id="49070-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="49070-109">Augmenter la sécurité</span><span class="sxs-lookup"><span data-stu-id="49070-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="49070-110">Mettre à l’échelle avec le libre-service</span><span class="sxs-lookup"><span data-stu-id="49070-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="49070-111">La définition d’un thème pour cadrer la preuve de concept vous aide à concentrer les efforts qui correspondent aux attentes l’entreprise, et qui souvent les déclencheurs de l’intérêt dans une preuve de concept en premier lieu.</span><span class="sxs-lookup"><span data-stu-id="49070-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="49070-112">Environnement</span><span class="sxs-lookup"><span data-stu-id="49070-112">Environment</span></span>

<span data-ttu-id="49070-113">Il est important de déterminer les détails de l’environnement dans lequel vous fournirez la preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="49070-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="49070-114">Idéalement, vous pouvez vous baser dessus une fois la preuve de concept terminée.</span><span class="sxs-lookup"><span data-stu-id="49070-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="49070-115">L’environnement cible est crucial, et vous devez trouver le juste équilibre entre une solution aussi réelle que possible et la charge des contraintes ou considérations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="49070-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="49070-116">Les environnements typiques pour les preuves de concept sont :</span><span class="sxs-lookup"><span data-stu-id="49070-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="49070-117">**Production :** Les scénarios seront implémentés dans votre environnement de production et les services cloud Microsoft déjà déployés (AD de production, Office 365, solution SSO/client Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49070-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="49070-118">**Test d’acceptation utilisateur (UAT)/Environnement de développement :** Vous disposez d’une infrastructure de test (Active Directory et éventuellement une solution SSO/client Azure AD en parallèle) avec des données de test qui ressemblent à celles de production.</span><span class="sxs-lookup"><span data-stu-id="49070-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="49070-119">En règle générale, l’environnement de test est partagé entre plusieurs projets dans l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="49070-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="49070-120">La plupart des scénarios de ce guide sont additifs par nature.</span><span class="sxs-lookup"><span data-stu-id="49070-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="49070-121">Par conséquent, ils peuvent être déployés dans le client de production sans affecter les utilisateurs en dehors de la preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="49070-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="49070-122">Dans ce document, nous évoquerons les scénarios qui auraient un impact sur l’ensemble du client.</span><span class="sxs-lookup"><span data-stu-id="49070-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="49070-123">Dans ce cas, vous souhaiterez envisager un environnement hors production.</span><span class="sxs-lookup"><span data-stu-id="49070-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="49070-124">Utilisateurs cible</span><span class="sxs-lookup"><span data-stu-id="49070-124">Target Users</span></span>

<span data-ttu-id="49070-125">Il est important de déterminer le jeu cible d’utilisateurs qui testeront les scénarios, en particulier lorsque l’environnement est en production ou en test.</span><span class="sxs-lookup"><span data-stu-id="49070-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="49070-126">Les catégories d’utilisateurs cibles pour les preuves de concept sont :</span><span class="sxs-lookup"><span data-stu-id="49070-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="49070-127">**Utilisateurs du pilote :** Les utilisateurs réels dans l’environnement qui utiliseront la solution avec le compte qu’ils utilisent pour leurs fonctions au quotidien</span><span class="sxs-lookup"><span data-stu-id="49070-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="49070-128">**Utilisateurs de test :** Les comptes de test créés dans l’environnement</span><span class="sxs-lookup"><span data-stu-id="49070-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="49070-129">La plupart des scénarios de ce guide peuvent être réalisés par des utilisateurs du pilote.</span><span class="sxs-lookup"><span data-stu-id="49070-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="49070-130">Dans ce document, nous évoquerons les considérations relatives aux utilisateurs cible si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="49070-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]