---
title: "Expressions conditionnelles du moteur de règles Azure CDN | Microsoft Docs"
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
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="bac9d-103">Expressions conditionnelles du moteur de règles Azure CDN</span><span class="sxs-lookup"><span data-stu-id="bac9d-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="bac9d-104">Cette rubrique répertorie les descriptions détaillées des expressions conditionnelles pour le [moteur de règles](cdn-rules-engine.md) Azure Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="bac9d-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="bac9d-105">La première partie d’une règle est l’expression conditionnelle.</span><span class="sxs-lookup"><span data-stu-id="bac9d-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="bac9d-106">Expression conditionnelle</span><span class="sxs-lookup"><span data-stu-id="bac9d-106">Conditional Expression</span></span> | <span data-ttu-id="bac9d-107">Description</span><span class="sxs-lookup"><span data-stu-id="bac9d-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="bac9d-108">IF</span><span class="sxs-lookup"><span data-stu-id="bac9d-108">IF</span></span> | <span data-ttu-id="bac9d-109">Une expression IF fait toujours partie de la première instruction dans une règle.</span><span class="sxs-lookup"><span data-stu-id="bac9d-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="bac9d-110">Comme toutes les autres expressions conditionnelles, cette instruction IF doit être associée à une correspondance.</span><span class="sxs-lookup"><span data-stu-id="bac9d-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="bac9d-111">Si aucune expression conditionnelle supplémentaire n’est définie, cette correspondance détermine le critère qui doit être remplie avant qu’un ensemble de fonctionnalités puisse être appliqué à une requête.</span><span class="sxs-lookup"><span data-stu-id="bac9d-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="bac9d-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="bac9d-112">AND IF</span></span> | <span data-ttu-id="bac9d-113">Une expression AND IF ne peut être ajoutée qu’après les types d’expressions conditionnelles suivants : IF, AND IF.</span><span class="sxs-lookup"><span data-stu-id="bac9d-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="bac9d-114">Elle indique qu’il existe une autre condition qui doit être remplie pour l’instruction IF initiale.</span><span class="sxs-lookup"><span data-stu-id="bac9d-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="bac9d-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="bac9d-115">ELSE IF</span></span>| <span data-ttu-id="bac9d-116">Une expression ELSE IF spécifie une autre condition qui doit être remplie avant la mise en place d’un ensemble de fonctionnalités spécifiques à cette instruction ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="bac9d-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="bac9d-117">La présence d’une instruction ELSE IF indique la fin de l’instruction précédente.</span><span class="sxs-lookup"><span data-stu-id="bac9d-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="bac9d-118">La seule expression conditionnelle pouvant être placée après une instruction ELSE IF est une autre instruction ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="bac9d-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="bac9d-119">Cela signifie qu’une instruction IF ELSE peut uniquement servir à spécifier une seule condition supplémentaire qui doit être respectée.</span><span class="sxs-lookup"><span data-stu-id="bac9d-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="bac9d-120">**Exemple** : ![condition de correspondance CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="bac9d-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="bac9d-121">Une règle ultérieure peut remplacer les actions spécifiées par une règle antérieure.</span><span class="sxs-lookup"><span data-stu-id="bac9d-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="bac9d-122">Exemple : une règle de fourre-tout sécurise toutes les requêtes par le biais de l’authentification basée sur un jeton.</span><span class="sxs-lookup"><span data-stu-id="bac9d-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="bac9d-123">Une autre règle peut être créée directement en dessous pour générer une exception pour certains types de requêtes.</span><span class="sxs-lookup"><span data-stu-id="bac9d-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="bac9d-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bac9d-124">Next steps</span></span>
* [<span data-ttu-id="bac9d-125">Vue d'ensemble d'Azure CDN</span><span class="sxs-lookup"><span data-stu-id="bac9d-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="bac9d-126">Référence du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="bac9d-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="bac9d-127">Conditions de correspondance du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="bac9d-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="bac9d-128">Fonctionnalités du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="bac9d-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="bac9d-129">Remplacement du comportement HTTP par défaut à l’aide du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="bac9d-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
