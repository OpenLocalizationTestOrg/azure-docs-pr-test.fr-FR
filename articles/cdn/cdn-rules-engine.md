---
title: "Remplacement du comportement HTTP à l’aide du moteur de règles Azure CDN | Microsoft Docs"
description: "Le moteur de règles vous permet de personnaliser la manière dont Azure CDN gère les requêtes HTTP, telles que le blocage de la remise de certains types de contenu, la définition d’une stratégie de mise en cache et la modification des en-têtes HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="a6f17-103">Remplacement du comportement HTTP à l’aide du moteur de règles Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a6f17-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="a6f17-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a6f17-104">Overview</span></span>
<span data-ttu-id="a6f17-105">Le moteur de règles vous permet de personnaliser comment sont gérées les requêtes HTTP, telles que le blocage de la remise de certains types de contenu, la définition d’une stratégie de mise en cache et la modification des en-têtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6f17-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="a6f17-106">Ce didacticiel présente la création d’une règle qui modifie le comportement de mise en cache des ressources CDN.</span><span class="sxs-lookup"><span data-stu-id="a6f17-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="a6f17-107">Du contenu vidéo est aussi disponible dans la section «[Voir aussi](#see-also)».</span><span class="sxs-lookup"><span data-stu-id="a6f17-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="a6f17-108">Pour obtenir une référence à la syntaxe détaillée, consultez [Référence du moteur de règles](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a6f17-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="a6f17-109">Didacticiel</span><span class="sxs-lookup"><span data-stu-id="a6f17-109">Tutorial</span></span>
1. <span data-ttu-id="a6f17-110">Dans le panneau de profil CDN, cliquez sur le bouton **Gérer** .</span><span class="sxs-lookup"><span data-stu-id="a6f17-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="a6f17-112">Le portail de gestion CDN s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="a6f17-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="a6f17-113">Cliquez sur l’onglet **HTTP volumineux**, puis sur **Moteur de règles**.</span><span class="sxs-lookup"><span data-stu-id="a6f17-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="a6f17-114">Les options d'une nouvelle règle s'affichent.</span><span class="sxs-lookup"><span data-stu-id="a6f17-114">Options for a new rule are displayed.</span></span>
   
    ![Options de nouvelle règle CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="a6f17-116">L'ordre dans lequel plusieurs règles sont répertoriées affecte la façon dont elles sont gérées.</span><span class="sxs-lookup"><span data-stu-id="a6f17-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="a6f17-117">Une règle ultérieure peut remplacer les actions spécifiées par une règle antérieure.</span><span class="sxs-lookup"><span data-stu-id="a6f17-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="a6f17-118">Entrez un nom dans la zone de texte **Nom / Description** .</span><span class="sxs-lookup"><span data-stu-id="a6f17-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="a6f17-119">Identifiez le type de requêtes auxquelles la règle s'applique.</span><span class="sxs-lookup"><span data-stu-id="a6f17-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="a6f17-120">Par défaut, la condition de correspondance **Toujours** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="a6f17-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="a6f17-121">Pour ce didacticiel, vous allez utiliser **Toujours** , donc conservez cette option.</span><span class="sxs-lookup"><span data-stu-id="a6f17-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condition de correspondance CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="a6f17-123">Il existe de nombreux types de condition de correspondance disponibles dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="a6f17-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="a6f17-124">Cliquez sur l'icône d'information bleue à gauche de la condition de correspondance pour obtenir une explication détaillée de la condition sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="a6f17-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="a6f17-125">Pour obtenir la liste complète des expressions conditionnelles en détail, consultez [Expressions conditionnelles du moteur de règles](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="a6f17-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="a6f17-126">Pour obtenir la liste complète des conditions de correspondance en détail, consultez [Conditions de correspondance du moteur de règles](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="a6f17-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="a6f17-127">Cliquez sur le bouton **+** en regard de **Fonctionnalités** pour ajouter une fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a6f17-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="a6f17-128">Dans la liste déroulante située à gauche, sélectionnez **Forcer l'âge maximal interne**.</span><span class="sxs-lookup"><span data-stu-id="a6f17-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="a6f17-129">Dans la zone de texte qui s'affiche, entrez **300**.</span><span class="sxs-lookup"><span data-stu-id="a6f17-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="a6f17-130">Conservez les valeurs par défaut restantes.</span><span class="sxs-lookup"><span data-stu-id="a6f17-130">Leave the remaining default values.</span></span>
   
   ![Fonctionnalité CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="a6f17-132">Comme avec les conditions de correspondance, en cliquez sur l'icône d'information bleue à gauche de la nouvelle fonctionnalité pour obtenir plus d'informations sur cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a6f17-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="a6f17-133">Dans le cas de **Forcer l’âge maximal interne**, nous remplaçons les en-têtes **Cache-Control** et **Expires** de la ressource, afin de contrôler quand le nœud de périmètre CDN actualise la ressource à partir de l’origine.</span><span class="sxs-lookup"><span data-stu-id="a6f17-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="a6f17-134">Notre exemple de 300 secondes signifie que le nœud de périmètre CDN met la ressource en cache pendant 5 minutes avant l'actualisation de la ressource à partir de son origine.</span><span class="sxs-lookup"><span data-stu-id="a6f17-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="a6f17-135">Pour obtenir la liste complète des fonctionnalités en détail, consultez [Informations sur les fonctionnalités du moteur de règles](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="a6f17-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="a6f17-136">Cliquez sur le bouton **Ajouter** pour enregistrer la nouvelle règle.</span><span class="sxs-lookup"><span data-stu-id="a6f17-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="a6f17-137">La nouvelle règle est en attente d'approbation.</span><span class="sxs-lookup"><span data-stu-id="a6f17-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="a6f17-138">Une fois qu’elle a été approuvée, l’état passe de **XML en attente** à **XML actif**.</span><span class="sxs-lookup"><span data-stu-id="a6f17-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a6f17-139">Les modifications de règles peuvent prendre jusqu’à 90 minutes avant d’être propagées à travers le CDN.</span><span class="sxs-lookup"><span data-stu-id="a6f17-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="a6f17-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a6f17-140">See also</span></span>
* [<span data-ttu-id="a6f17-141">Vue d'ensemble d'Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a6f17-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="a6f17-142">Référence du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="a6f17-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="a6f17-143">Conditions de correspondance du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="a6f17-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="a6f17-144">Expressions conditionnelles du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="a6f17-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="a6f17-145">Fonctionnalités du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="a6f17-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="a6f17-146">Remplacement du comportement HTTP par défaut à l’aide du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="a6f17-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="a6f17-147">[Azure Friday : les nouvelles fonctionnalités Premium puissantes du CDN Azure](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vidéo)</span><span class="sxs-lookup"><span data-stu-id="a6f17-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>