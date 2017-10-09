---
title: "les expressions conditionnelles du moteur de règles aaaAzure CDN | Documents Microsoft"
description: "Documentation de référence sur les fonctionnalités et conditions de correspondance du moteur de règles Azure CDN."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="2d929-103">Expressions conditionnelles du moteur de règles Azure CDN</span><span class="sxs-lookup"><span data-stu-id="2d929-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="2d929-104">Cette rubrique répertorie les descriptions détaillées de hello Expressions conditionnelles pour Azure réseau CDN (Content Delivery) [moteur de règles](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="2d929-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="2d929-105">Hello de première partie d’une règle est hello Expression conditionnelle.</span><span class="sxs-lookup"><span data-stu-id="2d929-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="2d929-106">Expression conditionnelle</span><span class="sxs-lookup"><span data-stu-id="2d929-106">Conditional Expression</span></span> | <span data-ttu-id="2d929-107">Description</span><span class="sxs-lookup"><span data-stu-id="2d929-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="2d929-108">IF</span><span class="sxs-lookup"><span data-stu-id="2d929-108">IF</span></span> | <span data-ttu-id="2d929-109">L’expression IF est toujours une partie de la première instruction de hello dans une règle.</span><span class="sxs-lookup"><span data-stu-id="2d929-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="2d929-110">Comme toutes les autres expressions conditionnelles, cette instruction IF doit être associée à une correspondance.</span><span class="sxs-lookup"><span data-stu-id="2d929-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="2d929-111">Si aucune des expressions conditionnelles supplémentaires ne sont définies, cette correspondance détermine le critère hello qui doit être remplie avant un ensemble de fonctionnalités peut-être être appliqués tooa demande.</span><span class="sxs-lookup"><span data-stu-id="2d929-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="2d929-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="2d929-112">AND IF</span></span> | <span data-ttu-id="2d929-113">L’expression IF et peut-être uniquement être ajoutée après hello suivant les types d’expressions conditionnel : IF, et si.</span><span class="sxs-lookup"><span data-stu-id="2d929-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="2d929-114">Il indique qu’il existe une autre condition qui doit être remplie pour une instruction IF initiale de hello.</span><span class="sxs-lookup"><span data-stu-id="2d929-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="2d929-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="2d929-115">ELSE IF</span></span>| <span data-ttu-id="2d929-116">Une expression ELSE IF spécifie une autre condition qui doit être remplie avant un ensemble de toothis spécifique de fonctionnalités instruction ELSE IF a lieu.</span><span class="sxs-lookup"><span data-stu-id="2d929-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="2d929-117">présence de Hello d’une instruction IF ELSE indique fin hello de l’instruction précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="2d929-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="2d929-118">Hello uniquement expression conditionnelle qui peut être placée après qu’une instruction IF ELSE est une autre instruction ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="2d929-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="2d929-119">Cela signifie qu’une instruction IF ELSE peut être uniquement toospecify utilisé une seule condition supplémentaire qui a toobe remplie.</span><span class="sxs-lookup"><span data-stu-id="2d929-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="2d929-120">**Exemple** : ![condition de correspondance CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="2d929-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="2d929-121">Une règle suivante peut remplacer les actions de hello spécifiées par une règle précédente.</span><span class="sxs-lookup"><span data-stu-id="2d929-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="2d929-122">Exemple : une règle de fourre-tout sécurise toutes les requêtes par le biais de l’authentification basée sur un jeton.</span><span class="sxs-lookup"><span data-stu-id="2d929-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="2d929-123">Une autre règle peut être créée directement en dessous toomake une exception pour certains types de demandes.</span><span class="sxs-lookup"><span data-stu-id="2d929-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="2d929-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d929-124">Next steps</span></span>
* [<span data-ttu-id="2d929-125">Vue d'ensemble d'Azure CDN</span><span class="sxs-lookup"><span data-stu-id="2d929-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="2d929-126">Référence du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="2d929-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="2d929-127">Conditions de correspondance du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="2d929-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="2d929-128">Fonctionnalités du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="2d929-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="2d929-129">Le comportement par défaut HTTP à l’aide du moteur de règles hello</span><span class="sxs-lookup"><span data-stu-id="2d929-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
