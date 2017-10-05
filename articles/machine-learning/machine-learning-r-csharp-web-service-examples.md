---
title: "(obsolète) Exemples de services web Machine Learning développés avec R - Azure | Microsoft Docs"
description: "(obsolète) Recherchez un ensemble pratique d’exemples de services web créés avec du code R et Machine Learning et publié sur Azure Marketplace."
keywords: csharp,code r,exemples de services web
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="41969-104">(obsolète) Des exemples de services web utilisant du code R sur Azure Machine Learning sont publiés sur Microsoft Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="41969-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="41969-105">Microsoft DataMarket va être mis hors service, et ces API sont désormais obsolètes.</span><span class="sxs-lookup"><span data-stu-id="41969-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="41969-106">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="41969-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="41969-107">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="41969-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="41969-108">Cet article contient des exemples de services web créés à l’aide d’Azure Machine Learning et publiés sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="41969-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="41969-109">Chaque exemple de service web est associé à un document complet intégrant des exemples de jeux de données pour tester les services et expliquant comment l’utilisateur peut lui-même créer un service similaire.</span><span class="sxs-lookup"><span data-stu-id="41969-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="41969-110">Dans Azure Machine Learning Studio, les utilisateurs peuvent écrire du code R et le publier en quelques clics sous la forme d’un service web afin que d’autres applications et périphériques l’utilisent dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="41969-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="41969-111">De la création de simples calculatrices qui fournissent des fonctionnalités de statistiques à la création d’un facteur personnalisé de prédiction d’analyse de sentiment dans l’exploration de textes, les utilisateurs R nouveaux et expérimentés peuvent bénéficier de la facilité avec laquelle les utilisateurs d’Azure Machine Learning exploitent le code R.</span><span class="sxs-lookup"><span data-stu-id="41969-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="41969-112">Bien que ces services web puissent être utilisés par les utilisateurs, via une application mobile ou un site web, l’objectif de ces exemples de services web est également de vous indiquer comment Machine Learning peut exploiter les scripts R à des fins analytiques et peut être utilisé pour créer des services web sur le code R.</span><span class="sxs-lookup"><span data-stu-id="41969-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="41969-113">Chaque exemple inclut un exemple C# de consommation du service web.</span><span class="sxs-lookup"><span data-stu-id="41969-113">Each example includes a C# example for web service consumption.</span></span>

![Diagramme du code R dans Azure Machine Learning : solutions R pour un usage propriétaire ou publiées sur Azure Marketplace.][1]

<span data-ttu-id="41969-115">Examinez les scénarios suivants.</span><span class="sxs-lookup"><span data-stu-id="41969-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="41969-116">Scénario 1 : modèle générique</span><span class="sxs-lookup"><span data-stu-id="41969-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="41969-117">Un utilisateur travaille avec un modèle générique qui peut être appliqué aux données d'un nouvel utilisateur, par exemple une prévision de données de série temporelles ou une méthode R personnalisée avec des analyses avancées.</span><span class="sxs-lookup"><span data-stu-id="41969-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="41969-118">Cet utilisateur publie le modèle sous forme de service web afin que d'autres utilisent ses données.</span><span class="sxs-lookup"><span data-stu-id="41969-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="41969-119">Classifieur binaire</span><span class="sxs-lookup"><span data-stu-id="41969-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="41969-120">Modèle de cluster</span><span class="sxs-lookup"><span data-stu-id="41969-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="41969-121">Régression linéaire multivariable</span><span class="sxs-lookup"><span data-stu-id="41969-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="41969-122">Prévisions : lissage exponentiel</span><span class="sxs-lookup"><span data-stu-id="41969-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="41969-123">Prévisions ETS + STL</span><span class="sxs-lookup"><span data-stu-id="41969-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="41969-124">Prévisions - Modèle ARIMA (Autoregressive Integrated Moving Average, moyenne mobile intégrée auto-régressive)</span><span class="sxs-lookup"><span data-stu-id="41969-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="41969-125">Analyse de survie</span><span class="sxs-lookup"><span data-stu-id="41969-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="41969-126">Scénario 2 : modèle formé : données spécifiques</span><span class="sxs-lookup"><span data-stu-id="41969-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="41969-127">Un utilisateur dispose de données qui fournissent des prédictions utiles dans le code R. Par exemple : un échantillon volumineux de questionnaires de personnalité regroupés via un algorithme à k moyennes pour prédire le type de personnalité de l’utilisateur ou des données d’enquête de santé qui peuvent être utilisées pour prédire le risque qu’un individu contracte un cancer du poumon, à l’aide d’un package R d’analyse de survie.</span><span class="sxs-lookup"><span data-stu-id="41969-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="41969-128">L'utilisateur publie les données via un service web qui prédit les résultats d'un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41969-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="41969-129">Scénario 3 : modèle formé : données génériques</span><span class="sxs-lookup"><span data-stu-id="41969-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="41969-130">Un utilisateur possède des données génériques (par exemple, un corpus de texte) qui permettent à un service web d’être développé et appliqué de manière générique dans différents types de scénarios et cas d’usage.</span><span class="sxs-lookup"><span data-stu-id="41969-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="41969-131">Analyse de sentiments basée sur un lexique</span><span class="sxs-lookup"><span data-stu-id="41969-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="41969-132">Scénario 4 : calculatrice avancée</span><span class="sxs-lookup"><span data-stu-id="41969-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="41969-133">Un utilisateur fournit des calculs complexes ou des simulations ne nécessitant aucun modèle formé ni ajustement d’un modèle pour les données de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41969-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="41969-134">Test de différence des proportions</span><span class="sxs-lookup"><span data-stu-id="41969-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="41969-135">Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="41969-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="41969-136">Suite de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="41969-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="41969-137">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="41969-137">FAQ</span></span>
<span data-ttu-id="41969-138">Pour les Questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="41969-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



