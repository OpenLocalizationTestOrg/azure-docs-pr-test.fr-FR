---
title: "aaaInteract avec des rapports à l’aide de hello API JavaScript | Documents Microsoft"
description: "Power BI Embedded, interagir avec les rapports à l’aide de hello API JavaScript"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="58c30-103">Interagir avec les rapports Power BI à l’aide de hello API JavaScript</span><span class="sxs-lookup"><span data-stu-id="58c30-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="58c30-104">Permet d’API de Power BI JavaScript Hello tooeasily vous incorporez des rapports Power BI dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="58c30-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="58c30-105">Avec l’API de hello, vos applications peuvent interagir par programme avec les différents éléments de rapport comme des pages et des filtres.</span><span class="sxs-lookup"><span data-stu-id="58c30-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="58c30-106">Cette interactivité intègre les rapports Power BI plus étroitement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="58c30-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="58c30-107">Vous incorporez un rapport Power BI dans votre application à l’aide d’un iframe qui est hébergé dans le cadre de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="58c30-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="58c30-108">Hello iframe agit comme une limite entre votre application et le rapport de hello, comme vous pouvez le voir Bonjour suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="58c30-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Iframe Power BI Embedded sans API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="58c30-110">Hello iframe fait hello incorporation processus beaucoup plus facile, mais sans hello d’API JavaScript hello rapport et votre application ne peut pas interagir avec eux.</span><span class="sxs-lookup"><span data-stu-id="58c30-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="58c30-111">Ce manque d’interaction peut rendre le sentiment rapport de hello ne faisait pas partie de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="58c30-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="58c30-112">application et les rapports hello réellement besoin toocommunicate dans les deux sens, comme dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="58c30-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Iframe Power BI Embedded avec API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="58c30-114">Hello JavaScript API de Power BI vous permet de code toowrite en toute sécurité traverser les limites d’iframe hello.</span><span class="sxs-lookup"><span data-stu-id="58c30-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="58c30-115">Cela permet tooprogrammatically de votre application réaliser une action dans un rapport et toolisten pour les événements des actions effectuées par les utilisateurs au sein du rapport de hello.</span><span class="sxs-lookup"><span data-stu-id="58c30-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="58c30-116">Que pouvez-vous faire avec hello JavaScript API de Power BI ?</span><span class="sxs-lookup"><span data-stu-id="58c30-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="58c30-117">Avec hello API JavaScript, vous pouvez gérer des rapports, accédez toopages dans un rapport, filtrer un rapport et gérer l’incorporation des événements.</span><span class="sxs-lookup"><span data-stu-id="58c30-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="58c30-118">Hello diagramme suivant montre structure hello Hello API.</span><span class="sxs-lookup"><span data-stu-id="58c30-118">hello following diagram shows hello structure of hello API.</span></span>

![Diagramme de l’API JavaScript de Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="58c30-120">Gérer les rapports</span><span class="sxs-lookup"><span data-stu-id="58c30-120">Manage reports</span></span>
<span data-ttu-id="58c30-121">Hello API Javascript vous permet de comportement toomanage au niveau de rapport et de page hello :</span><span class="sxs-lookup"><span data-stu-id="58c30-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="58c30-122">Incorporer un rapport Power BI en toute sécurité dans votre application - essayez de hello [incorporer l’application de démonstration](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="58c30-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="58c30-123">Définir le jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="58c30-123">Set access token</span></span>
* <span data-ttu-id="58c30-124">Configurer les rapports de hello</span><span class="sxs-lookup"><span data-stu-id="58c30-124">Configure hello report</span></span>
  * <span data-ttu-id="58c30-125">Activer et désactiver le volet de filtre hello et le volet de navigation de page : essayez hello [mettre à jour d’application de démonstration de paramètres](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="58c30-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="58c30-126">Définir les valeurs par défaut des pages et des filtres - essayez de hello [ensemble démo sur les valeurs par défaut](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="58c30-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="58c30-127">Afficher et quitter le mode plein écran</span><span class="sxs-lookup"><span data-stu-id="58c30-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="58c30-128">En savoir plus sur l’incorporation d’un rapport</span><span class="sxs-lookup"><span data-stu-id="58c30-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="58c30-129">Accédez toopages dans un rapport</span><span class="sxs-lookup"><span data-stu-id="58c30-129">Navigate toopages in a report</span></span>
<span data-ttu-id="58c30-130">Hello API JavaScript enbales vous toodiscover toutes les pages dans un rapport et tooset hello actuel une page.</span><span class="sxs-lookup"><span data-stu-id="58c30-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="58c30-131">Essayez de hello [application de démonstration de navigation](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="58c30-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="58c30-132">En savoir plus sur la navigation entre les pages</span><span class="sxs-lookup"><span data-stu-id="58c30-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="58c30-133">Filtrer un rapport</span><span class="sxs-lookup"><span data-stu-id="58c30-133">Filter a report</span></span>
<span data-ttu-id="58c30-134">Hello API JavaScript fournit de base et avancés des fonctionnalités pour les rapports intégrés et les pages du rapport de filtre.</span><span class="sxs-lookup"><span data-stu-id="58c30-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="58c30-135">Essayez de hello [le filtrage d’application de démonstration](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)et passez en revue du code introduction ici.</span><span class="sxs-lookup"><span data-stu-id="58c30-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="58c30-136">Filtres de base</span><span class="sxs-lookup"><span data-stu-id="58c30-136">Basic filters</span></span>
<span data-ttu-id="58c30-137">Un filtre de base est placé sur un niveau de la colonne ou de la hiérarchie et contient une liste de valeurs tooinclude ou exclure.</span><span class="sxs-lookup"><span data-stu-id="58c30-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="58c30-138">Filtres avancés</span><span class="sxs-lookup"><span data-stu-id="58c30-138">Advanced filters</span></span>
<span data-ttu-id="58c30-139">Les filtres avancés utilisent l’opérateur logique de hello et ou ou et acceptez les conditions d’une ou deux, chacun avec leur propre opérateur et la valeur.</span><span class="sxs-lookup"><span data-stu-id="58c30-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="58c30-140">Les conditions prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="58c30-140">Supported conditions are:</span></span>

* <span data-ttu-id="58c30-141">Aucun</span><span class="sxs-lookup"><span data-stu-id="58c30-141">None</span></span>
* <span data-ttu-id="58c30-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="58c30-142">LessThan</span></span>
* <span data-ttu-id="58c30-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="58c30-143">LessThanOrEqual</span></span>
* <span data-ttu-id="58c30-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="58c30-144">GreaterThan</span></span>
* <span data-ttu-id="58c30-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="58c30-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="58c30-146">Contient</span><span class="sxs-lookup"><span data-stu-id="58c30-146">Contains</span></span>
* <span data-ttu-id="58c30-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="58c30-147">DoesNotContain</span></span>
* <span data-ttu-id="58c30-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="58c30-148">StartsWith</span></span>
* <span data-ttu-id="58c30-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="58c30-149">DoesNotStartWith</span></span>
* <span data-ttu-id="58c30-150">Is</span><span class="sxs-lookup"><span data-stu-id="58c30-150">Is</span></span>
* <span data-ttu-id="58c30-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="58c30-151">IsNot</span></span>
* <span data-ttu-id="58c30-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="58c30-152">IsBlank</span></span>
* <span data-ttu-id="58c30-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="58c30-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="58c30-154">En savoir plus sur le filtrage</span><span class="sxs-lookup"><span data-stu-id="58c30-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="58c30-155">Gestion des événements</span><span class="sxs-lookup"><span data-stu-id="58c30-155">Handling events</span></span>
<span data-ttu-id="58c30-156">En outre informations toosending dans hello iframe, votre application peut également recevoir des informations sur hello suivant des événements provenant de hello iframe :</span><span class="sxs-lookup"><span data-stu-id="58c30-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="58c30-157">Embed</span><span class="sxs-lookup"><span data-stu-id="58c30-157">Embed</span></span>
  * <span data-ttu-id="58c30-158">chargé</span><span class="sxs-lookup"><span data-stu-id="58c30-158">loaded</span></span>
  * <span data-ttu-id="58c30-159">error</span><span class="sxs-lookup"><span data-stu-id="58c30-159">error</span></span>
* <span data-ttu-id="58c30-160">Rapports</span><span class="sxs-lookup"><span data-stu-id="58c30-160">Reports</span></span>
  * <span data-ttu-id="58c30-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="58c30-161">pageChanged</span></span>
  * <span data-ttu-id="58c30-162">dataSelected (disponible prochainement)</span><span class="sxs-lookup"><span data-stu-id="58c30-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="58c30-163">En savoir plus sur la gestion des événements</span><span class="sxs-lookup"><span data-stu-id="58c30-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="58c30-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58c30-164">Next steps</span></span>
<span data-ttu-id="58c30-165">Pour plus d’informations sur hello JavaScript API de Power BI, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="58c30-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="58c30-166">Wiki d’API JavaScript</span><span class="sxs-lookup"><span data-stu-id="58c30-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="58c30-167">Référence du modèle d’objet</span><span class="sxs-lookup"><span data-stu-id="58c30-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="58c30-168">Exemples</span><span class="sxs-lookup"><span data-stu-id="58c30-168">Samples</span></span>
  * [<span data-ttu-id="58c30-169">Angular</span><span class="sxs-lookup"><span data-stu-id="58c30-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="58c30-170">Ember</span><span class="sxs-lookup"><span data-stu-id="58c30-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="58c30-171">Démonstration en direct</span><span class="sxs-lookup"><span data-stu-id="58c30-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

