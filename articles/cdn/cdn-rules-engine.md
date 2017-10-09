---
title: "comportement aaaOverride HTTP à l’aide du moteur de règles d’Azure CDN hello | Documents Microsoft"
description: "moteur de règles Hello vous permet de toocustomize comment les requêtes HTTP sont gérés par le CDN Azure, telles que le blocage de remise hello de certains types de contenu, définir une stratégie de mise en cache et modifier les en-têtes HTTP."
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
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="ced0c-103">Remplacer le comportement HTTP à l’aide du moteur de règles hello CDN Azure</span><span class="sxs-lookup"><span data-stu-id="ced0c-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="ced0c-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ced0c-104">Overview</span></span>
<span data-ttu-id="ced0c-105">moteur de règles Hello vous permet de toocustomize comment sont gérées les demandes HTTP, telles que le blocage remise hello de certains types de contenu, la définition d’une stratégie de mise en cache et la modification des en-têtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ced0c-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="ced0c-106">Ce didacticiel va vous montrer la création d’une règle modifiera hello mise en cache de comportement des composants CDN.</span><span class="sxs-lookup"><span data-stu-id="ced0c-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="ced0c-107">Contenu vidéo est également disponible dans hello »[Voir aussi](#see-also)« section.</span><span class="sxs-lookup"><span data-stu-id="ced0c-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="ced0c-108">Pour une syntaxe de toohello référence détaillée, consultez [référence du moteur de règles](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ced0c-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="ced0c-109">Didacticiel</span><span class="sxs-lookup"><span data-stu-id="ced0c-109">Tutorial</span></span>
1. <span data-ttu-id="ced0c-110">À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.</span><span class="sxs-lookup"><span data-stu-id="ced0c-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="ced0c-112">portail de gestion CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="ced0c-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="ced0c-113">Cliquez sur hello **grand HTTP** onglet, suivi **moteur de règles**.</span><span class="sxs-lookup"><span data-stu-id="ced0c-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="ced0c-114">Les options d'une nouvelle règle s'affichent.</span><span class="sxs-lookup"><span data-stu-id="ced0c-114">Options for a new rule are displayed.</span></span>
   
    ![Options de nouvelle règle CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="ced0c-116">commande Hello dans lequel plusieurs règles sont répertoriés affecte comment elles sont gérées.</span><span class="sxs-lookup"><span data-stu-id="ced0c-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="ced0c-117">Une règle suivante peut remplacer les actions de hello spécifiées par une règle précédente.</span><span class="sxs-lookup"><span data-stu-id="ced0c-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="ced0c-118">Entrez un nom dans hello **nom / Description** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ced0c-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="ced0c-119">Identifier le type hello de hello règle s’applique à des demandes.</span><span class="sxs-lookup"><span data-stu-id="ced0c-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="ced0c-120">Par défaut, hello **toujours** condition de correspondance est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="ced0c-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="ced0c-121">Pour ce didacticiel, vous allez utiliser **Toujours** , donc conservez cette option.</span><span class="sxs-lookup"><span data-stu-id="ced0c-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condition de correspondance CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="ced0c-123">Il existe de nombreux types de correspondance conditions disponibles dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="ced0c-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="ced0c-124">En cliquant sur hello bleu icône d’information toohello gauche de la condition de correspondance hello explique condition hello actuellement sélectionné en détail.</span><span class="sxs-lookup"><span data-stu-id="ced0c-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="ced0c-125">Pour hello une liste complète des expressions conditionnelles en détail, consultez [Expressions conditionnelles du moteur de règles](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="ced0c-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="ced0c-126">Pour hello une liste complète des conditions de correspondance en détail, consultez [condition correspond à moteur de règles](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="ced0c-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="ced0c-127">Cliquez sur hello  **+**  bouton ensuite trop**fonctionnalités** tooadd une nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ced0c-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="ced0c-128">Dans la liste déroulante hello hello gauche, sélectionnez **Force interne Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="ced0c-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="ced0c-129">Dans la zone de texte hello qui s’affiche, entrez **300**.</span><span class="sxs-lookup"><span data-stu-id="ced0c-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="ced0c-130">Laissez hello restant des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="ced0c-130">Leave hello remaining default values.</span></span>
   
   ![Fonctionnalité CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="ced0c-132">Comme avec les conditions de correspondance, en cliquant sur toohello d’icône d’information hello bleue à gauche de hello nouvelle fonctionnalité affichera les détails sur cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ced0c-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="ced0c-133">Dans les cas de hello de **Force interne Max-Age**, nous allons substitution de l’élément multimédia hello **Cache-Control** et **Expires** en-têtes toocontrol lorsque le nœud de périmètre CDN hello actualisera hello ressource à partir de l’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="ced0c-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="ced0c-134">Notre exemple de 300 secondes signifie le nœud de périmètre CDN hello mettra en cache les ressources hello pendant 5 minutes avant d’actualiser asset hello à partir de son origine.</span><span class="sxs-lookup"><span data-stu-id="ced0c-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="ced0c-135">Pour hello une liste complète des fonctionnalités en détail, consultez [les détails sur les fonctionnalités du moteur de règles](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="ced0c-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="ced0c-136">Cliquez sur hello **ajouter** nouvelle règle bouton toosave hello.</span><span class="sxs-lookup"><span data-stu-id="ced0c-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="ced0c-137">nouvelle règle de Hello est maintenant en attente d’approbation.</span><span class="sxs-lookup"><span data-stu-id="ced0c-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="ced0c-138">Une fois qu’elle a été approuvée, hello statut deviendra **XML en attente** trop**XML Active**.</span><span class="sxs-lookup"><span data-stu-id="ced0c-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ced0c-139">Les modifications de règles peuvent prendre jusqu'à toopropagate de minutes too90 via hello CDN.</span><span class="sxs-lookup"><span data-stu-id="ced0c-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="ced0c-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ced0c-140">See also</span></span>
* [<span data-ttu-id="ced0c-141">Vue d'ensemble d'Azure CDN</span><span class="sxs-lookup"><span data-stu-id="ced0c-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="ced0c-142">Référence du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="ced0c-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="ced0c-143">Conditions de correspondance du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="ced0c-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="ced0c-144">Expressions conditionnelles du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="ced0c-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="ced0c-145">Fonctionnalités du moteur de règles</span><span class="sxs-lookup"><span data-stu-id="ced0c-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="ced0c-146">Le comportement par défaut HTTP à l’aide du moteur de règles hello</span><span class="sxs-lookup"><span data-stu-id="ced0c-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="ced0c-147">[Azure Friday : les nouvelles fonctionnalités Premium puissantes du CDN Azure](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vidéo)</span><span class="sxs-lookup"><span data-stu-id="ced0c-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>