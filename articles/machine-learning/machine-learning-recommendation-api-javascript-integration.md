---
title: "Machine Learning Recommendations : intégration à l’aide de JavaScript | Microsoft Docs"
description: "Azure Machine Learning Recommendations - Intégration à l’aide de JavaScript - documentation"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="9dc22-103">Azure Machine Learning Recommendations - Intégration à l’aide de JavaScript</span><span class="sxs-lookup"><span data-stu-id="9dc22-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="9dc22-104">Vous devez commencer à utiliser le Service cognitif de l’API Recommandations au lieu de cette version.</span><span class="sxs-lookup"><span data-stu-id="9dc22-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="9dc22-105">Le Service cognitif de l’API Recommandations remplacera ce service et toutes les nouvelles fonctionnalités y seront développées.</span><span class="sxs-lookup"><span data-stu-id="9dc22-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="9dc22-106">Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.</span><span class="sxs-lookup"><span data-stu-id="9dc22-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="9dc22-107">En savoir plus sur la [migration vers le nouveau Service cognitif](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="9dc22-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="9dc22-108">Ce document décrit comment intégrer votre site à l’aide de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9dc22-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="9dc22-109">JavaScript vous permet d’envoyer des événements d’acquisition de données et d’utiliser les recommandations après la génération d’un modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="9dc22-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="9dc22-110">Toutes les opérations effectuées via JS peuvent également être effectuées côté serveur.</span><span class="sxs-lookup"><span data-stu-id="9dc22-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="9dc22-111">1. Présentation générale</span><span class="sxs-lookup"><span data-stu-id="9dc22-111">1. General Overview</span></span>
<span data-ttu-id="9dc22-112">L’intégration de votre site avec Azure ML Recommandations se compose de 2 phases :</span><span class="sxs-lookup"><span data-stu-id="9dc22-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="9dc22-113">Envoi d’événements dans Azure ML Recommendations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="9dc22-114">Cela permet de générer un modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="9dc22-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="9dc22-115">Utilisation des recommandations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-115">Consume the recommendations.</span></span> <span data-ttu-id="9dc22-116">Une fois le modèle créé, vous pouvez utiliser les recommandations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="9dc22-117">(Ce document n’explique pas comment générer un modèle, lisez le guide de démarrage rapide pour obtenir plus d’informations à ce sujet).</span><span class="sxs-lookup"><span data-stu-id="9dc22-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="9dc22-118"><ins>Phase I</ins></span><span class="sxs-lookup"><span data-stu-id="9dc22-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="9dc22-119">Dans la première phase, vous insérez dans vos pages html une petite bibliothèque JavaScript qui permet à la page d’envoyer des événements se produisant sur une page html vers les serveurs Azure ML Recommandations (via Data Market) :</span><span class="sxs-lookup"><span data-stu-id="9dc22-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="9dc22-121"><ins>Phase II</ins></span><span class="sxs-lookup"><span data-stu-id="9dc22-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="9dc22-122">Pendant la deuxième phase, lorsque vous souhaitez afficher les recommandations sur la page, sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="9dc22-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="9dc22-123">1. Votre serveur (dans la phase de rendu des pages) appelle le serveur Azure ML Recommandations (via Data Market) pour obtenir des recommandations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="9dc22-124">Les résultats incluent une liste des ID d’articles.</span><span class="sxs-lookup"><span data-stu-id="9dc22-124">The results include a list of items id.</span></span> <span data-ttu-id="9dc22-125">Votre serveur a besoin d’enrichir les résultats avec les métadonnées des articles (par exemple des images, une description) et d’envoyer la page créée dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="9dc22-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Drawing2][2]

<span data-ttu-id="9dc22-127">2. L’autre option consiste à utiliser le petit fichier JavaScript de la première étape pour obtenir une liste simple d’articles recommandés.</span><span class="sxs-lookup"><span data-stu-id="9dc22-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="9dc22-128">Les données reçues ici sont moins conséquentes qu’avec la première option.</span><span class="sxs-lookup"><span data-stu-id="9dc22-128">The data received here is leaner than the one in the first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="9dc22-130">2. Prérequis</span><span class="sxs-lookup"><span data-stu-id="9dc22-130">2. Prerequisites</span></span>
1. <span data-ttu-id="9dc22-131">Créer un nouveau modèle à l’aide des API.</span><span class="sxs-lookup"><span data-stu-id="9dc22-131">Create a new model using the APIs.</span></span> <span data-ttu-id="9dc22-132">Consultez le guide de démarrage rapide pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="9dc22-133">Encodez votre &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; avec base64.</span><span class="sxs-lookup"><span data-stu-id="9dc22-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="9dc22-134">(Cela est utilisé pour l’authentification de base afin d’autoriser le code JS à appeler les API).</span><span class="sxs-lookup"><span data-stu-id="9dc22-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="9dc22-135">3. Envoyer des événements d’acquisition de données à l’aide de JavaScript</span><span class="sxs-lookup"><span data-stu-id="9dc22-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="9dc22-136">Les étapes suivantes facilitent l’envoi d’événements :</span><span class="sxs-lookup"><span data-stu-id="9dc22-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="9dc22-137">Incluez la bibliothèque JQuery dans votre code.</span><span class="sxs-lookup"><span data-stu-id="9dc22-137">Include JQuery library in your code.</span></span> <span data-ttu-id="9dc22-138">Vous pouvez la télécharger à partir de nuget sur l’URL suivante.</span><span class="sxs-lookup"><span data-stu-id="9dc22-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="9dc22-139">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="9dc22-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="9dc22-140">Incluez la bibliothèque JavaScript Recommandations depuis l’URL suivante : http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="9dc22-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="9dc22-141">Initialisez la bibliothèque Azure ML Recommandations avec les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="9dc22-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="9dc22-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<ID_modèle>"); </script>
4. Envoyez l’événement approprié.</span><span class="sxs-lookup"><span data-stu-id="9dc22-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="9dc22-143">Consultez la section détaillée ci-dessous sur tous les types d’événements (exemple d’événement Click) <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="9dc22-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="9dc22-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="9dc22-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="9dc22-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="9dc22-145">3.1.</span></span>    <span data-ttu-id="9dc22-146">Limitations et prise en charge du navigateur</span><span class="sxs-lookup"><span data-stu-id="9dc22-146">Limitations and Browser Support</span></span>
<span data-ttu-id="9dc22-147">Il s’agit d’une implémentation de référence, fournie en l’état.</span><span class="sxs-lookup"><span data-stu-id="9dc22-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="9dc22-148">Elle prend normalement en charge les principaux navigateurs.</span><span class="sxs-lookup"><span data-stu-id="9dc22-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="9dc22-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="9dc22-149">3.2.</span></span>    <span data-ttu-id="9dc22-150">Type d’événements</span><span class="sxs-lookup"><span data-stu-id="9dc22-150">Type of Events</span></span>
<span data-ttu-id="9dc22-151">Il existe cinq types d’événements pris en charge par la bibliothèque : clic, clic de recommandation, ajouter au panier, supprimer du panier et achat.</span><span class="sxs-lookup"><span data-stu-id="9dc22-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="9dc22-152">Il existe un événement supplémentaire, utilisé pour définir le contexte utilisateur, appelé connexion.</span><span class="sxs-lookup"><span data-stu-id="9dc22-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="9dc22-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="9dc22-153">3.2.1.</span></span> <span data-ttu-id="9dc22-154">Événement clic</span><span class="sxs-lookup"><span data-stu-id="9dc22-154">Click Event</span></span>
<span data-ttu-id="9dc22-155">Cet événement doit être utilisé chaque fois qu’un utilisateur clique sur un article.</span><span class="sxs-lookup"><span data-stu-id="9dc22-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="9dc22-156">Généralement lorsque l’utilisateur clique sur un article, une nouvelle page s’ouvre avec les détails de l’article ; cet événement doit être déclenché dans cette page.</span><span class="sxs-lookup"><span data-stu-id="9dc22-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="9dc22-157">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="9dc22-157">Parameters:</span></span>

* <span data-ttu-id="9dc22-158">event (chaîne, obligatoire) - “click”</span><span class="sxs-lookup"><span data-stu-id="9dc22-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="9dc22-159">item (chaîne, obligatoire) - identificateur unique de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="9dc22-160">itemName (chaîne, facultatif) - nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="9dc22-161">itemDescription (chaîne, facultatif) - description de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="9dc22-162">itemCategory (chaîne, facultatif) - catégorie de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="9dc22-163">Ou avec des données facultatives :</span><span class="sxs-lookup"><span data-stu-id="9dc22-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="9dc22-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="9dc22-164">3.2.2.</span></span> <span data-ttu-id="9dc22-165">Événement clic de recommandation</span><span class="sxs-lookup"><span data-stu-id="9dc22-165">Recommendation Click Event</span></span>
<span data-ttu-id="9dc22-166">Cet événement doit être utilisé chaque fois qu’un utilisateur clique sur un article recommandé reçu à partir d’Azure ML Recommandations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="9dc22-167">Généralement lorsque l’utilisateur clique sur un article, une nouvelle page s’ouvre avec les détails de l’article ; cet événement doit être déclenché dans cette page.</span><span class="sxs-lookup"><span data-stu-id="9dc22-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="9dc22-168">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="9dc22-168">Parameters:</span></span>

* <span data-ttu-id="9dc22-169">event (chaîne, obligatoire) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="9dc22-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="9dc22-170">item (chaîne, obligatoire) - identificateur unique de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="9dc22-171">itemName (chaîne, facultatif) - nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="9dc22-172">itemDescription (chaîne, facultatif) - description de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="9dc22-173">itemCategory (chaîne, facultatif) - catégorie de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="9dc22-174">seeds (tableau de chaînes, facultatif) - valeurs initiales qui ont généré la requête de recommandation.</span><span class="sxs-lookup"><span data-stu-id="9dc22-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="9dc22-175">recoList (tableau de chaînes, facultatif) - résultat de la demande de recommandation qui a généré l'élément cliqué.</span><span class="sxs-lookup"><span data-stu-id="9dc22-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="9dc22-176">Ou avec des données facultatives :</span><span class="sxs-lookup"><span data-stu-id="9dc22-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="9dc22-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="9dc22-177">3.2.3.</span></span> <span data-ttu-id="9dc22-178">Événement ajouter au panier</span><span class="sxs-lookup"><span data-stu-id="9dc22-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="9dc22-179">Cet événement doit être utilisé lorsque l’utilisateur ajoute un article au panier.</span><span class="sxs-lookup"><span data-stu-id="9dc22-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="9dc22-180">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="9dc22-180">Parameters:</span></span>

* <span data-ttu-id="9dc22-181">event (chaîne, obligatoire) - “addshopcart”</span><span class="sxs-lookup"><span data-stu-id="9dc22-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="9dc22-182">item (chaîne, obligatoire) - identificateur unique de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="9dc22-183">itemName (chaîne, facultatif) - nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="9dc22-184">itemDescription (chaîne, facultatif) - description de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="9dc22-185">itemCategory (chaîne, facultatif) - catégorie de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="9dc22-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="9dc22-186">3.2.4.</span></span> <span data-ttu-id="9dc22-187">Événement supprimer du panier</span><span class="sxs-lookup"><span data-stu-id="9dc22-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="9dc22-188">Cet événement doit être utilisé lorsque l’utilisateur supprime un article du panier.</span><span class="sxs-lookup"><span data-stu-id="9dc22-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="9dc22-189">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="9dc22-189">Parameters:</span></span>

* <span data-ttu-id="9dc22-190">event (chaîne, obligatoire) - “removeshopcart”</span><span class="sxs-lookup"><span data-stu-id="9dc22-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="9dc22-191">item (chaîne, obligatoire) - identificateur unique de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="9dc22-192">itemName (chaîne, facultatif) - nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="9dc22-193">itemDescription (chaîne, facultatif) - description de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="9dc22-194">itemCategory (chaîne, facultatif) - catégorie de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="9dc22-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="9dc22-195">3.2.5.</span></span> <span data-ttu-id="9dc22-196">Événement d’achat</span><span class="sxs-lookup"><span data-stu-id="9dc22-196">Purchase Event</span></span>
<span data-ttu-id="9dc22-197">Cet événement doit être utilisé lorsque l’utilisateur achète son panier.</span><span class="sxs-lookup"><span data-stu-id="9dc22-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="9dc22-198">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="9dc22-198">Parameters:</span></span>

* <span data-ttu-id="9dc22-199">event (chaîne) - “purchase”</span><span class="sxs-lookup"><span data-stu-id="9dc22-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="9dc22-200">items ( Purchased ) - Tableau contenant une entrée pour chaque article acheté.</span><span class="sxs-lookup"><span data-stu-id="9dc22-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="9dc22-201">Format d’achat :</span><span class="sxs-lookup"><span data-stu-id="9dc22-201">Purchased format:</span></span>
  * <span data-ttu-id="9dc22-202">item (chaîne) – identificateur unique de l'élément.</span><span class="sxs-lookup"><span data-stu-id="9dc22-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="9dc22-203">count (entier ou chaîne) - nombre d'articles achetés.</span><span class="sxs-lookup"><span data-stu-id="9dc22-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="9dc22-204">price (flottant ou chaîne) - champ facultatif - prix de l'élément.</span><span class="sxs-lookup"><span data-stu-id="9dc22-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="9dc22-205">L’exemple suivant présente l’achat de 3 articles (33, 34, 35), dont deux avec tous les champs renseignés (article, quantité, prix) et l’autre (article 34) sans prix.</span><span class="sxs-lookup"><span data-stu-id="9dc22-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="9dc22-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="9dc22-206">3.2.6.</span></span> <span data-ttu-id="9dc22-207">Événement de connexion utilisateur</span><span class="sxs-lookup"><span data-stu-id="9dc22-207">User Login Event</span></span>
<span data-ttu-id="9dc22-208">La bibliothèque d’événements ML Azure Recommandations crée et utilise un cookie afin d’identifier les événements provenant du même navigateur.</span><span class="sxs-lookup"><span data-stu-id="9dc22-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="9dc22-209">Afin d’améliorer les résultats du modèle, Azure ML Recommandations permet de définir une identification unique de l’utilisateur qui remplace l’utilisation de cookies.</span><span class="sxs-lookup"><span data-stu-id="9dc22-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="9dc22-210">Cet événement doit être utilisé après la connexion utilisateur à votre site.</span><span class="sxs-lookup"><span data-stu-id="9dc22-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="9dc22-211">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="9dc22-211">Parameters:</span></span>

* <span data-ttu-id="9dc22-212">event (chaîne) - “userlogin”</span><span class="sxs-lookup"><span data-stu-id="9dc22-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="9dc22-213">user (chaîne) - identification unique de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9dc22-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="9dc22-214">4. Utiliser les recommandations via JavaScript</span><span class="sxs-lookup"><span data-stu-id="9dc22-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="9dc22-215">Le code qui utilise les recommandations est déclenché par un événement JavaScript de la page Web du client.</span><span class="sxs-lookup"><span data-stu-id="9dc22-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="9dc22-216">La réponse de recommandation inclut les ID des articles recommandés, leurs noms et leurs évaluations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="9dc22-217">Il est préférable d’utiliser cette option uniquement pour afficher les articles recommandés sous forme de liste : les opérations de gestion plus complexes (par exemple l’ajout de métadonnées de l’article) doivent être effectuées sur l’intégration du côté serveur.</span><span class="sxs-lookup"><span data-stu-id="9dc22-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="9dc22-218">4.1 Utilisation des recommandations</span><span class="sxs-lookup"><span data-stu-id="9dc22-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="9dc22-219">Pour utiliser des recommandations, vous devez inclure les bibliothèques JavaScript requises sur votre page et appeler AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="9dc22-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="9dc22-220">Consultez la section 2.</span><span class="sxs-lookup"><span data-stu-id="9dc22-220">See section 2.</span></span>

<span data-ttu-id="9dc22-221">Pour utiliser des recommandations pour un ou plusieurs articles, vous devez appeler une méthode nommée : AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="9dc22-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="9dc22-222">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="9dc22-222">Parameters:</span></span>

* <span data-ttu-id="9dc22-223">articles (table de chaînes) - un ou plusieurs articles pour lesquels vous souhaitez obtenir des recommandations.</span><span class="sxs-lookup"><span data-stu-id="9dc22-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="9dc22-224">Si vous consommez une build Fbt, vous ne pouvez définir qu'un seul élément ici.</span><span class="sxs-lookup"><span data-stu-id="9dc22-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="9dc22-225">numberOfResults (entier) - nombre de résultats requis.</span><span class="sxs-lookup"><span data-stu-id="9dc22-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="9dc22-226">includeMetadata (booléen, facultatif) - si « true », indique que le champ de métadonnées doit être rempli dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="9dc22-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="9dc22-227">Fonction de traitement - fonction qui gérera les recommandations renvoyées.</span><span class="sxs-lookup"><span data-stu-id="9dc22-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="9dc22-228">Les données sont retournées sous forme de tableau de :</span><span class="sxs-lookup"><span data-stu-id="9dc22-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="9dc22-229">Item - ID unique de l’élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-229">Item - item unique id</span></span>
  * <span data-ttu-id="9dc22-230">name - nom de l'élément (s’il existe dans le catalogue)</span><span class="sxs-lookup"><span data-stu-id="9dc22-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="9dc22-231">rating - évaluation de la recommandation</span><span class="sxs-lookup"><span data-stu-id="9dc22-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="9dc22-232">métadonnées - chaîne qui représente les métadonnées de l'élément</span><span class="sxs-lookup"><span data-stu-id="9dc22-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="9dc22-233">Exemple : le code suivant demande 8 recommandations pour l’article « 64f6eb0d-947a-4c18-a16c-888da9e228ba » (et en ne spécifiant pas includeMetadata, il indique implicitement qu’aucune métadonnée n’est requise). Il concatène ensuite les résultats dans une mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="9dc22-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
