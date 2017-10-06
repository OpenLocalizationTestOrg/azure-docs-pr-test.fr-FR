---
title: "aaaAzure Active Directory preuve de concept manuel d’ingrédients | Documents Microsoft"
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
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="db4d3-104">Ingrédients du manuel de preuve de concept Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db4d3-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="db4d3-105">Thème</span><span class="sxs-lookup"><span data-stu-id="db4d3-105">Theme</span></span>
<span data-ttu-id="db4d3-106">Azure AD fournit des solutions d’identité et accès dans plusieurs domaines d’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="db4d3-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="db4d3-107">Nous allons classifier scénarios hello Bonjour suivant de zones :</span><span class="sxs-lookup"><span data-stu-id="db4d3-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="db4d3-108">Un grand nombre d’applications, une seule identité</span><span class="sxs-lookup"><span data-stu-id="db4d3-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="db4d3-109">Augmenter la sécurité</span><span class="sxs-lookup"><span data-stu-id="db4d3-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="db4d3-110">Mettre à l’échelle avec le libre-service</span><span class="sxs-lookup"><span data-stu-id="db4d3-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="db4d3-111">Définissez un Bonjour de tooframe de thème que preuve de concept vous aide aux efforts de hello toofocus correspond aux attentes des objectifs de l’entreprise, qui sont souvent déclencheurs hello intérêt hello dans une preuve de concept dans le premier emplacement dans hello.</span><span class="sxs-lookup"><span data-stu-id="db4d3-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="db4d3-112">Environnement</span><span class="sxs-lookup"><span data-stu-id="db4d3-112">Environment</span></span>

<span data-ttu-id="db4d3-113">Il est important toodetermine hello des informations sur hello environnement où vous fournira hello preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="db4d3-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="db4d3-114">Dans l’idéal, vous pouvez générer lui après hello que preuve de concept est terminée.</span><span class="sxs-lookup"><span data-stu-id="db4d3-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="db4d3-115">environnement cible de Hello est primordial et que vous devez rechercher hello juste équilibre entre effectuer il réel que possible et surcharge hello des contraintes ou des considérations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="db4d3-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="db4d3-116">environnements de type Hello pour la validation des conceptions sont :</span><span class="sxs-lookup"><span data-stu-id="db4d3-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="db4d3-117">**Production :** les scénarios hello sera implémentés dans votre environnement d’exploitation et déjà déployé les services de Cloud Microsoft (solution de production AD, Office 365, Azure AD client / l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="db4d3-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="db4d3-118">**Test d’acceptation utilisateur (UAT)/Environnement de développement :** Vous disposez d’une infrastructure de test (Active Directory et éventuellement une solution SSO/client Azure AD en parallèle) avec des données de test qui ressemblent à celles de production.</span><span class="sxs-lookup"><span data-stu-id="db4d3-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="db4d3-119">En général, environnement de test hello est partagé entre plusieurs projets dans l’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="db4d3-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="db4d3-120">La plupart des scénarios de ce guide sont additifs par nature.</span><span class="sxs-lookup"><span data-stu-id="db4d3-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="db4d3-121">Par conséquent, ils peuvent être déployés dans le client de production hello sans affecter les utilisateurs en dehors de la preuve de concept de hello.</span><span class="sxs-lookup"><span data-stu-id="db4d3-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="db4d3-122">Dans ce document, nous évoquerons les scénarios qui auraient un impact sur l’ensemble du client.</span><span class="sxs-lookup"><span data-stu-id="db4d3-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="db4d3-123">Dans ce cas, vous pourriez tooconsider un environnement hors production.</span><span class="sxs-lookup"><span data-stu-id="db4d3-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="db4d3-124">Utilisateurs cible</span><span class="sxs-lookup"><span data-stu-id="db4d3-124">Target Users</span></span>

<span data-ttu-id="db4d3-125">Il est le jeu de cibles hello toodetermine important d’utilisateurs qui vérifient les scénarios de hello, en particulier lorsque l’environnement de hello est production ou test.</span><span class="sxs-lookup"><span data-stu-id="db4d3-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="db4d3-126">Hello des catégories d’utilisateurs cibles de preuve de concept sont :</span><span class="sxs-lookup"><span data-stu-id="db4d3-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="db4d3-127">**Utilisateurs du pilote :** fonctions de travail des utilisateurs réels dans l’environnement hello qui utilisent des solutions de hello avec compte hello qu’ils utilisent pour leur tooday jour</span><span class="sxs-lookup"><span data-stu-id="db4d3-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="db4d3-128">**Les utilisateurs de test :** comptes créés dans hello environnement de Test</span><span class="sxs-lookup"><span data-stu-id="db4d3-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="db4d3-129">La plupart des scénarios de ce guide peuvent être réalisés par des utilisateurs du pilote.</span><span class="sxs-lookup"><span data-stu-id="db4d3-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="db4d3-130">Dans ce document, nous évoquerons les considérations relatives aux utilisateurs cible si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="db4d3-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]