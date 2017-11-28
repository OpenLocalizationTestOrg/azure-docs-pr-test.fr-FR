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
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="2efbc-103">Azure Machine Learning Recommendations - Intégration à l’aide de JavaScript</span><span class="sxs-lookup"><span data-stu-id="2efbc-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="2efbc-104">Vous devez commencer à l’aide de hello Service cognitifs de recommandations API au lieu de cette version.</span><span class="sxs-lookup"><span data-stu-id="2efbc-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="2efbc-105">Hello Service cognitifs recommandations remplacera ce service et toutes les hello nouvelles fonctionnalités seront développées il.</span><span class="sxs-lookup"><span data-stu-id="2efbc-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="2efbc-106">Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.</span><span class="sxs-lookup"><span data-stu-id="2efbc-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="2efbc-107">En savoir plus sur [migration toohello nouveau Service cognitifs](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="2efbc-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="2efbc-108">Ce document décrivent comment toointegrate votre site à l’aide de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2efbc-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="2efbc-109">Hello JavaScript vous permet de toosend les événements d’Acquisition de données et les recommandations de tooconsume une fois que vous générez un modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="2efbc-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="2efbc-110">Toutes les opérations effectuées via JS peuvent également être effectuées côté serveur.</span><span class="sxs-lookup"><span data-stu-id="2efbc-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="2efbc-111">1. Présentation générale</span><span class="sxs-lookup"><span data-stu-id="2efbc-111">1. General Overview</span></span>
<span data-ttu-id="2efbc-112">L’intégration de votre site avec Azure ML Recommandations se compose de 2 phases :</span><span class="sxs-lookup"><span data-stu-id="2efbc-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="2efbc-113">Envoi d’événements dans Azure ML Recommendations.</span><span class="sxs-lookup"><span data-stu-id="2efbc-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="2efbc-114">Cette opération activera toobuild un modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="2efbc-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="2efbc-115">Utiliser les recommandations hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-115">Consume hello recommendations.</span></span> <span data-ttu-id="2efbc-116">Après la génération de modèle de hello, vous pouvez utiliser les recommandations hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="2efbc-117">(Ce document n’explique pas comment toobuild un modèle, lire hello tooget guide de démarrage rapide plus d’informations sur la façon de).</span><span class="sxs-lookup"><span data-stu-id="2efbc-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="2efbc-118"><ins>Phase I</ins></span><span class="sxs-lookup"><span data-stu-id="2efbc-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="2efbc-119">Bonjour première phase, de que vous insérez dans vos pages html une petite bibliothèque JavaScript qui permet hello événements de page toosend qu’ils se produisent sur une page html de hello en tant que serveurs Azure ML recommandations (via Data Market) :</span><span class="sxs-lookup"><span data-stu-id="2efbc-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="2efbc-121"><ins>Phase II</ins></span><span class="sxs-lookup"><span data-stu-id="2efbc-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="2efbc-122">Bonjour deuxième phase, lorsque vous souhaitez que les recommandations de hello tooshow sur la page de hello vous sélectionnez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="2efbc-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="2efbc-123">1. votre serveur (sur la phase de hello de rendu de page) appelle recommandations tooget de serveur de recommandations Azure ML (via Data Market).</span><span class="sxs-lookup"><span data-stu-id="2efbc-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="2efbc-124">les résultats de Hello incluent une liste des id d’éléments. Votre serveur a besoin des résultats de hello tooenrich avec hello des éléments de métadonnées (par exemple, les images, description) et envoyer hello créé de page toohello navigateur.</span><span class="sxs-lookup"><span data-stu-id="2efbc-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Drawing2][2]

<span data-ttu-id="2efbc-126">2. hello autre option est toouse hello JavaScript fichier de petite taille à partir de la phase d’un tooget une simple liste d’éléments recommandés.</span><span class="sxs-lookup"><span data-stu-id="2efbc-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="2efbc-127">les données de salutation reçues ici sont très optimisées à hello une option de première hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="2efbc-129">2. Composants requis</span><span class="sxs-lookup"><span data-stu-id="2efbc-129">2. Prerequisites</span></span>
1. <span data-ttu-id="2efbc-130">Créer un modèle à l’aide des API de hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="2efbc-131">Consultez le guide de démarrage rapide hello sur la façon de toodo il.</span><span class="sxs-lookup"><span data-stu-id="2efbc-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="2efbc-132">Encodez votre &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; avec base64.</span><span class="sxs-lookup"><span data-stu-id="2efbc-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="2efbc-133">(Cela sera utilisé pour hello l’authentification de base tooenable hello JS code toocall hello API).</span><span class="sxs-lookup"><span data-stu-id="2efbc-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="2efbc-134">3. Envoyer des événements d’acquisition de données à l’aide de JavaScript</span><span class="sxs-lookup"><span data-stu-id="2efbc-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="2efbc-135">Hello suit facilite l’envoi d’événements :</span><span class="sxs-lookup"><span data-stu-id="2efbc-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="2efbc-136">Incluez la bibliothèque JQuery dans votre code.</span><span class="sxs-lookup"><span data-stu-id="2efbc-136">Include JQuery library in your code.</span></span> <span data-ttu-id="2efbc-137">Vous pouvez le télécharger à partir de nuget Bonjour suivant l’URL.</span><span class="sxs-lookup"><span data-stu-id="2efbc-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="2efbc-138">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="2efbc-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="2efbc-139">Inclure bibliothèque de Script de recommandations Java hello de hello suivant URL : http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="2efbc-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="2efbc-140">Initialisation de la bibliothèque d’Azure ML recommandations avec les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="2efbc-141"><script>AzureMLRecommendationsStart («<base64encoding of username:key>», « < model_id > ») ; </script> 
4. Événement approprié d’envoi hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="2efbc-142">Consultez la section détaillée ci-dessous sur tous les types d’événements (exemple d’événement Click) <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="2efbc-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="2efbc-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="2efbc-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="2efbc-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="2efbc-144">3.1.</span></span>    <span data-ttu-id="2efbc-145">Limitations et prise en charge du navigateur</span><span class="sxs-lookup"><span data-stu-id="2efbc-145">Limitations and Browser Support</span></span>
<span data-ttu-id="2efbc-146">Il s’agit d’une implémentation de référence, fournie en l’état.</span><span class="sxs-lookup"><span data-stu-id="2efbc-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="2efbc-147">Elle prend normalement en charge les principaux navigateurs.</span><span class="sxs-lookup"><span data-stu-id="2efbc-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="2efbc-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="2efbc-148">3.2.</span></span>    <span data-ttu-id="2efbc-149">Type d’événements</span><span class="sxs-lookup"><span data-stu-id="2efbc-149">Type of Events</span></span>
<span data-ttu-id="2efbc-150">Il existe 5 types d’événement qui prend en charge de la bibliothèque de hello : cliquez sur, la recommandation, cliquez sur, ajouter tooShop panier d’achat, supprimer de panier d’usine et d’achat.</span><span class="sxs-lookup"><span data-stu-id="2efbc-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="2efbc-151">Il existe un événement supplémentaire qui est utilisé tooset hello utilisateur contexte appelé compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="2efbc-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="2efbc-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="2efbc-152">3.2.1.</span></span> <span data-ttu-id="2efbc-153">Événement clic</span><span class="sxs-lookup"><span data-stu-id="2efbc-153">Click Event</span></span>
<span data-ttu-id="2efbc-154">Cet événement doit être utilisé chaque fois qu’un utilisateur clique sur un article.</span><span class="sxs-lookup"><span data-stu-id="2efbc-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="2efbc-155">En général lorsque l’utilisateur clique sur un élément une nouvelle page est ouvert avec les détails de l’élément hello ; Cet événement doit être déclenché dans cette page.</span><span class="sxs-lookup"><span data-stu-id="2efbc-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="2efbc-156">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="2efbc-156">Parameters:</span></span>

* <span data-ttu-id="2efbc-157">event (chaîne, obligatoire) - “click”</span><span class="sxs-lookup"><span data-stu-id="2efbc-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="2efbc-158">élément (string, obligatoire) - identificateur Unique de l’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="2efbc-159">nom de l’élément (string, facultatif) - nom hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="2efbc-160">DescriptionArticle (string, facultatif) - description hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="2efbc-161">itemCategory (string, facultatif) - catégorie hello de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="2efbc-162">Ou avec des données facultatives :</span><span class="sxs-lookup"><span data-stu-id="2efbc-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="2efbc-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="2efbc-163">3.2.2.</span></span> <span data-ttu-id="2efbc-164">Événement clic de recommandation</span><span class="sxs-lookup"><span data-stu-id="2efbc-164">Recommendation Click Event</span></span>
<span data-ttu-id="2efbc-165">Cet événement doit être utilisé chaque fois qu’un utilisateur clique sur un article recommandé reçu à partir d’Azure ML Recommandations.</span><span class="sxs-lookup"><span data-stu-id="2efbc-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="2efbc-166">En général lorsque l’utilisateur clique sur un élément une nouvelle page est ouvert avec les détails de l’élément hello ; Cet événement doit être déclenché dans cette page.</span><span class="sxs-lookup"><span data-stu-id="2efbc-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="2efbc-167">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="2efbc-167">Parameters:</span></span>

* <span data-ttu-id="2efbc-168">event (chaîne, obligatoire) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="2efbc-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="2efbc-169">élément (string, obligatoire) - identificateur Unique de l’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="2efbc-170">nom de l’élément (string, facultatif) - nom hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="2efbc-171">DescriptionArticle (string, facultatif) - description hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="2efbc-172">itemCategory (string, facultatif) - catégorie hello de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="2efbc-173">semences (tableau de chaînes, facultatif) - hello semences qui a généré la requête de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="2efbc-174">recoList (tableau de chaînes, facultatif) - hello du résultat de demande de recommandation hello qui a généré l’élément hello que l’utilisateur a cliqué.</span><span class="sxs-lookup"><span data-stu-id="2efbc-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="2efbc-175">Ou avec des données facultatives :</span><span class="sxs-lookup"><span data-stu-id="2efbc-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="2efbc-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="2efbc-176">3.2.3.</span></span> <span data-ttu-id="2efbc-177">Événement ajouter au panier</span><span class="sxs-lookup"><span data-stu-id="2efbc-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="2efbc-178">Cet événement doit être utilisé lorsque l’utilisateur hello ajouter un toohello élément panier d’achat.</span><span class="sxs-lookup"><span data-stu-id="2efbc-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="2efbc-179">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="2efbc-179">Parameters:</span></span>

* <span data-ttu-id="2efbc-180">event (chaîne, obligatoire) - “addshopcart”</span><span class="sxs-lookup"><span data-stu-id="2efbc-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="2efbc-181">élément (string, obligatoire) - identificateur Unique de l’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="2efbc-182">nom de l’élément (string, facultatif) - nom hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="2efbc-183">DescriptionArticle (string, facultatif) - description hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="2efbc-184">itemCategory (string, facultatif) - catégorie hello de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="2efbc-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="2efbc-185">3.2.4.</span></span> <span data-ttu-id="2efbc-186">Événement supprimer du panier</span><span class="sxs-lookup"><span data-stu-id="2efbc-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="2efbc-187">Cet événement doit être utilisé lorsque l’utilisateur de hello supprime un élément toohello panier d’achat.</span><span class="sxs-lookup"><span data-stu-id="2efbc-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="2efbc-188">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="2efbc-188">Parameters:</span></span>

* <span data-ttu-id="2efbc-189">event (chaîne, obligatoire) - “removeshopcart”</span><span class="sxs-lookup"><span data-stu-id="2efbc-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="2efbc-190">élément (string, obligatoire) - identificateur Unique de l’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="2efbc-191">nom de l’élément (string, facultatif) - nom hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="2efbc-192">DescriptionArticle (string, facultatif) - description hello d’élément de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="2efbc-193">itemCategory (string, facultatif) - catégorie hello de hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="2efbc-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="2efbc-194">3.2.5.</span></span> <span data-ttu-id="2efbc-195">Événement d’achat</span><span class="sxs-lookup"><span data-stu-id="2efbc-195">Purchase Event</span></span>
<span data-ttu-id="2efbc-196">Cet événement doit être utilisé lors de l’utilisateur de hello achat son panier d’achat.</span><span class="sxs-lookup"><span data-stu-id="2efbc-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="2efbc-197">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="2efbc-197">Parameters:</span></span>

* <span data-ttu-id="2efbc-198">event (chaîne) - “purchase”</span><span class="sxs-lookup"><span data-stu-id="2efbc-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="2efbc-199">items ( Purchased ) - Tableau contenant une entrée pour chaque article acheté.</span><span class="sxs-lookup"><span data-stu-id="2efbc-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="2efbc-200">Format d’achat :</span><span class="sxs-lookup"><span data-stu-id="2efbc-200">Purchased format:</span></span>
  * <span data-ttu-id="2efbc-201">élément (chaîne), un identificateur Unique de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="2efbc-202">count (entier ou chaîne) - nombre d'articles achetés.</span><span class="sxs-lookup"><span data-stu-id="2efbc-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="2efbc-203">prix (float ou string) - champ facultatif - hello prix de hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="2efbc-204">exemple Hello ci-dessous montre l’achat de 3 éléments (33, 34, 35), deux avec tous les champs renseignés (élément, nombre, prix) et l’autre (élément 34) sans un prix.</span><span class="sxs-lookup"><span data-stu-id="2efbc-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="2efbc-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="2efbc-205">3.2.6.</span></span> <span data-ttu-id="2efbc-206">Événement de connexion utilisateur</span><span class="sxs-lookup"><span data-stu-id="2efbc-206">User Login Event</span></span>
<span data-ttu-id="2efbc-207">Azure ML événement de recommandations bibliothèque crée et utiliser un cookie dans les événements de tooidentify commande provenant hello même navigateur.</span><span class="sxs-lookup"><span data-stu-id="2efbc-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="2efbc-208">Dans le modèle hello tooimprove résultats Azure ML recommandations permet tooset une identification unique utilisateur qui remplace l’utilisation du cookie hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="2efbc-209">Cet événement doit être utilisé après le site de tooyour de connexion de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="2efbc-210">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="2efbc-210">Parameters:</span></span>

* <span data-ttu-id="2efbc-211">event (chaîne) - “userlogin”</span><span class="sxs-lookup"><span data-stu-id="2efbc-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="2efbc-212">utilisateur (chaîne), une identification unique de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="2efbc-213">4. Utiliser les recommandations via JavaScript</span><span class="sxs-lookup"><span data-stu-id="2efbc-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="2efbc-214">code Hello qui consomme la recommandation de hello est déclenché par un événement JavaScript par la page Web de hello client.</span><span class="sxs-lookup"><span data-stu-id="2efbc-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="2efbc-215">réponse de recommandation Hello inclut hello ID des éléments, leurs noms et leurs classements recommandés.</span><span class="sxs-lookup"><span data-stu-id="2efbc-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="2efbc-216">Il s’agit des meilleures toouse cette option uniquement pour un affichage de liste de hello recommandé des éléments - plus complexes à gérer (par exemple, l’ajout de métadonnées de l’élément hello) doit être effectuée sur l’intégration de côté serveur hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="2efbc-217">4.1 Utilisation des recommandations</span><span class="sxs-lookup"><span data-stu-id="2efbc-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="2efbc-218">recommandations tooconsume que vous devez tooinclude hello requis des bibliothèques JavaScript dans votre page et de toocall AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="2efbc-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="2efbc-219">Consultez la section 2.</span><span class="sxs-lookup"><span data-stu-id="2efbc-219">See section 2.</span></span>

<span data-ttu-id="2efbc-220">recommandations tooconsume pour un ou plusieurs éléments, vous devez toocall une méthode appelée : AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="2efbc-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="2efbc-221">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="2efbc-221">Parameters:</span></span>

* <span data-ttu-id="2efbc-222">Un ou plusieurs éléments tooget recommandations relatives à des éléments (tableau de chaînes -).</span><span class="sxs-lookup"><span data-stu-id="2efbc-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="2efbc-223">Si vous consommez une build Fbt, vous ne pouvez définir qu'un seul élément ici.</span><span class="sxs-lookup"><span data-stu-id="2efbc-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="2efbc-224">numberOfResults (entier) - nombre de résultats requis.</span><span class="sxs-lookup"><span data-stu-id="2efbc-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="2efbc-225">includeMetadata (boolean, facultatif) - si définir too'true' indique ce champ de métadonnées hello doit être rempli dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="2efbc-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="2efbc-226">Fonction de traitement - une fonction qui gérera les recommandations hello renvoyées.</span><span class="sxs-lookup"><span data-stu-id="2efbc-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="2efbc-227">les données de salutation sont retournées sous forme de tableau de :</span><span class="sxs-lookup"><span data-stu-id="2efbc-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="2efbc-228">Item - ID unique de l’élément</span><span class="sxs-lookup"><span data-stu-id="2efbc-228">Item - item unique id</span></span>
  * <span data-ttu-id="2efbc-229">name - nom de l'élément (s’il existe dans le catalogue)</span><span class="sxs-lookup"><span data-stu-id="2efbc-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="2efbc-230">rating - évaluation de la recommandation</span><span class="sxs-lookup"><span data-stu-id="2efbc-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="2efbc-231">métadonnées - une chaîne qui représente les métadonnées d’élément de hello hello</span><span class="sxs-lookup"><span data-stu-id="2efbc-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="2efbc-232">Exemple : hello suivant code demande 8 recommandations pour l’élément « 64f6eb0d-947a-4c18-a16c-888da9e228ba » (et en ne spécifiant includeMetadata - implicitement indique qu’aucune métadonnée n’est nécessaire), puis, il concaténer les résultats hello dans une mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="2efbc-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

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
