---
title: "Interagir avec des rapports Power BI à l’aide de l’API JavaScript | Microsoft Docs"
description: "Power BI Embedded, interagit avec des rapports à l’aide de l’API JavaScript"
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
ms.openlocfilehash: 500462ac835674d80650c02aa7fc629b4a975857
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="interact-with-power-bi-reports-using-the-javascript-api"></a><span data-ttu-id="53231-103">Interagir avec des rapports Power BI à l’aide de l’API JavaScript</span><span class="sxs-lookup"><span data-stu-id="53231-103">Interact with Power BI reports using the JavaScript API</span></span>
<span data-ttu-id="53231-104">L’API JavaScript de Power BI vous permet d’incorporer facilement des rapports Power BI dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="53231-104">The Power BI JavaScript API enables you to easily embed Power BI reports into your applications.</span></span> <span data-ttu-id="53231-105">Avec l’API, vos applications peuvent interagir par programmation avec différents éléments d’un rapport, comme des pages et des filtres.</span><span class="sxs-lookup"><span data-stu-id="53231-105">With the API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="53231-106">Cette interactivité intègre les rapports Power BI plus étroitement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="53231-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="53231-107">Vous incorporez un rapport Power BI dans votre application en utilisant un iframe qui est hébergé dans le cadre de l’application.</span><span class="sxs-lookup"><span data-stu-id="53231-107">You embed a Power BI report in your application by using an iframe that is hosted as part of the application.</span></span> <span data-ttu-id="53231-108">Comme vous pouvez le voir dans l’image suivante, l’iframe agit comme une barrière entre votre application et le rapport.</span><span class="sxs-lookup"><span data-stu-id="53231-108">The iframe acts as a boundary between your application and the report, as you can see in the following image.</span></span> 

![Iframe Power BI Embedded sans API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="53231-110">L’iframe facilite considérablement le processus d’incorporation, mais sans l’API JavaScript, le rapport et votre application ne peuvent pas interagir entre eux.</span><span class="sxs-lookup"><span data-stu-id="53231-110">The iframe makes the embedding process a lot easier, but without the JavaScript API the report and your application can't interact with each other.</span></span> <span data-ttu-id="53231-111">Ce manque d’interaction peut faire penser que le rapport ne fait pas vraiment partie de l’application.</span><span class="sxs-lookup"><span data-stu-id="53231-111">This lack of interaction can make it feel like the report is not really part of the application.</span></span> <span data-ttu-id="53231-112">Le rapport et l’application doivent véritablement communiquer entre eux, comme dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="53231-112">The report and application really need to communicate back and forth, as in the following image.</span></span>

![Iframe Power BI Embedded avec API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="53231-114">L’API JavaScript de Power BI vous permet d’écrire du code capable de traverser en toute sécurité la limite de l’iframe.</span><span class="sxs-lookup"><span data-stu-id="53231-114">The Power BI JavaScript API enables you to write code that can securely pass through the iframe boundary.</span></span> <span data-ttu-id="53231-115">Cela permet à votre application d’exécuter par programmation une action dans un rapport et d’écouter des événements sur les actions effectuées par les utilisateurs dans le rapport.</span><span class="sxs-lookup"><span data-stu-id="53231-115">This enables your application to programmatically perform an action in a report, and to listen for events from actions that users make within the report.</span></span>

## <a name="what-can-you-do-with-the-power-bi-javascript-api"></a><span data-ttu-id="53231-116">Que pouvez-vous faire avec l’API JavaScript de Power BI ?</span><span class="sxs-lookup"><span data-stu-id="53231-116">What can you do with the Power BI JavaScript API?</span></span>
<span data-ttu-id="53231-117">Avec l’API JavaScript, vous pouvez gérer des rapports, accéder aux pages d’un rapport, filtrer un rapport et gérer l’incorporation des événements.</span><span class="sxs-lookup"><span data-stu-id="53231-117">With the JavaScript API you can manage reports, navigate to pages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="53231-118">Le schéma suivant présente la structure de l’API.</span><span class="sxs-lookup"><span data-stu-id="53231-118">The following diagram shows the structure of the API.</span></span>

![Diagramme de l’API JavaScript de Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="53231-120">Gérer les rapports</span><span class="sxs-lookup"><span data-stu-id="53231-120">Manage reports</span></span>
<span data-ttu-id="53231-121">L’API Javascript vous permet de gérer le comportement au niveau du rapport et de la page :</span><span class="sxs-lookup"><span data-stu-id="53231-121">The Javascript API enables you to manage behavior at the report and page level:</span></span>

* <span data-ttu-id="53231-122">Incorporer un rapport Power BI spécifique en toute sécurité dans votre application : essayer l’ [application de démonstration Embed](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="53231-122">Embed a specific Power BI Report securely in your application - try the [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="53231-123">Définir le jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="53231-123">Set access token</span></span>
* <span data-ttu-id="53231-124">Configurer le rapport</span><span class="sxs-lookup"><span data-stu-id="53231-124">Configure the report</span></span>
  * <span data-ttu-id="53231-125">Activer et désactiver le volet de filtre et le volet de navigation entre les pages : essayez l’ [application de démonstration Update Settings](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="53231-125">Enable and disable the filter pane and page navigation pane - try the [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="53231-126">Définir les valeurs par défaut des pages et des filtres : essayez l’ [application de démonstration Set Defaults](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="53231-126">Set defaults for pages and filters - try the [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="53231-127">Afficher et quitter le mode plein écran</span><span class="sxs-lookup"><span data-stu-id="53231-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="53231-128">En savoir plus sur l’incorporation d’un rapport</span><span class="sxs-lookup"><span data-stu-id="53231-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-to-pages-in-a-report"></a><span data-ttu-id="53231-129">Accéder aux pages d’un rapport</span><span class="sxs-lookup"><span data-stu-id="53231-129">Navigate to pages in a report</span></span>
<span data-ttu-id="53231-130">L’API JavaScript vous permet de découvrir toutes les pages d’un rapport et de définir la page actuelle.</span><span class="sxs-lookup"><span data-stu-id="53231-130">The JavaScript API enbales you to discover all pages in a report and to set the current page.</span></span> <span data-ttu-id="53231-131">Essayez l’ [application de démonstration Navigation](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="53231-131">Try the [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="53231-132">En savoir plus sur la navigation entre les pages</span><span class="sxs-lookup"><span data-stu-id="53231-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="53231-133">Filtrer un rapport</span><span class="sxs-lookup"><span data-stu-id="53231-133">Filter a report</span></span>
<span data-ttu-id="53231-134">L’API JavaScript fournit les fonctionnalités de filtrage de base et avancées pour les rapports incorporés et les pages de rapport.</span><span class="sxs-lookup"><span data-stu-id="53231-134">The JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="53231-135">Essayez l’ [application de démonstration Filter](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)et examinez le code de présentation ici.</span><span class="sxs-lookup"><span data-stu-id="53231-135">Try the [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="53231-136">Filtres de base</span><span class="sxs-lookup"><span data-stu-id="53231-136">Basic filters</span></span>
<span data-ttu-id="53231-137">Un filtre de base est placé sur une colonne ou un niveau hiérarchique, et contient une liste de valeurs à inclure ou exclure.</span><span class="sxs-lookup"><span data-stu-id="53231-137">A basic filter is placed on a column or hierarchy level and contains a list of values to include or exclude.</span></span>

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


#### <a name="advanced-filters"></a><span data-ttu-id="53231-138">Filtres avancés</span><span class="sxs-lookup"><span data-stu-id="53231-138">Advanced filters</span></span>
<span data-ttu-id="53231-139">Les filtres avancés utilisent l’opérateur logique AND ou OR, et acceptent une ou deux conditions, chacune avec son propre opérateur et sa propre valeur.</span><span class="sxs-lookup"><span data-stu-id="53231-139">Advanced filters use the logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="53231-140">Les conditions prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="53231-140">Supported conditions are:</span></span>

* <span data-ttu-id="53231-141">Aucun</span><span class="sxs-lookup"><span data-stu-id="53231-141">None</span></span>
* <span data-ttu-id="53231-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="53231-142">LessThan</span></span>
* <span data-ttu-id="53231-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="53231-143">LessThanOrEqual</span></span>
* <span data-ttu-id="53231-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="53231-144">GreaterThan</span></span>
* <span data-ttu-id="53231-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="53231-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="53231-146">Contient</span><span class="sxs-lookup"><span data-stu-id="53231-146">Contains</span></span>
* <span data-ttu-id="53231-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="53231-147">DoesNotContain</span></span>
* <span data-ttu-id="53231-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="53231-148">StartsWith</span></span>
* <span data-ttu-id="53231-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="53231-149">DoesNotStartWith</span></span>
* <span data-ttu-id="53231-150">Is</span><span class="sxs-lookup"><span data-stu-id="53231-150">Is</span></span>
* <span data-ttu-id="53231-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="53231-151">IsNot</span></span>
* <span data-ttu-id="53231-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="53231-152">IsBlank</span></span>
* <span data-ttu-id="53231-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="53231-153">IsNotBlank</span></span>

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
[<span data-ttu-id="53231-154">En savoir plus sur le filtrage</span><span class="sxs-lookup"><span data-stu-id="53231-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="53231-155">Gestion des événements</span><span class="sxs-lookup"><span data-stu-id="53231-155">Handling events</span></span>
<span data-ttu-id="53231-156">Outre l’envoi d’informations dans l’iframe, votre application peut également recevoir des informations sur les événements suivants provenant de l’iframe :</span><span class="sxs-lookup"><span data-stu-id="53231-156">In addition to sending information into the iframe, your application can also receive information on the following events coming from the iframe:</span></span>

* <span data-ttu-id="53231-157">Embed</span><span class="sxs-lookup"><span data-stu-id="53231-157">Embed</span></span>
  * <span data-ttu-id="53231-158">chargé</span><span class="sxs-lookup"><span data-stu-id="53231-158">loaded</span></span>
  * <span data-ttu-id="53231-159">error</span><span class="sxs-lookup"><span data-stu-id="53231-159">error</span></span>
* <span data-ttu-id="53231-160">Rapports</span><span class="sxs-lookup"><span data-stu-id="53231-160">Reports</span></span>
  * <span data-ttu-id="53231-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="53231-161">pageChanged</span></span>
  * <span data-ttu-id="53231-162">dataSelected (disponible prochainement)</span><span class="sxs-lookup"><span data-stu-id="53231-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="53231-163">En savoir plus sur la gestion des événements</span><span class="sxs-lookup"><span data-stu-id="53231-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="53231-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53231-164">Next steps</span></span>
<span data-ttu-id="53231-165">Pour plus d’informations sur l’API JavaScript de Power BI, cliquez sur les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="53231-165">For more information about the Power BI JavaScript API, check out the following links:</span></span>

* [<span data-ttu-id="53231-166">Wiki d’API JavaScript</span><span class="sxs-lookup"><span data-stu-id="53231-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="53231-167">Référence du modèle d’objet</span><span class="sxs-lookup"><span data-stu-id="53231-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="53231-168">Exemples</span><span class="sxs-lookup"><span data-stu-id="53231-168">Samples</span></span>
  * [<span data-ttu-id="53231-169">Angular</span><span class="sxs-lookup"><span data-stu-id="53231-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="53231-170">Ember</span><span class="sxs-lookup"><span data-stu-id="53231-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="53231-171">Démonstration en direct</span><span class="sxs-lookup"><span data-stu-id="53231-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

