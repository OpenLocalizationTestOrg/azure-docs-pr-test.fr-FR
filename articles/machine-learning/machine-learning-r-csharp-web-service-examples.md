---
title: "AAA(deprecated) Machine learning web services exemples générés avec R - Azure | Documents Microsoft"
description: "(déconseillée) Rechercher un ensemble utile des exemples de services web créés avec le code R et l’apprentissage et publié toohello Azure Marketplace."
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
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="9ed4f-104">(déconseillée) Exemples d’utilisation de code R dans Azure Machine Learning et publié tooMicrosoft Azure Marketplace de services Web</span><span class="sxs-lookup"><span data-stu-id="9ed4f-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="9ed4f-105">Hello Microsoft DataMarket a été supprimée et ces API ont été déconseillées.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="9ed4f-106">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9ed4f-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9ed4f-107">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="9ed4f-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9ed4f-108">Dans cet article sont web d’exemple services ont été créés à l’aide d’Azure Machine Learning et publié toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="9ed4f-109">Chaque exemple de service web a un document complet attaché, l’incorporation des jeux de données d’exemple pour le test des services de hello et expliquant comment hello utilisateur peut créer un service similaire eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="9ed4f-110">Dans Azure Machine Learning Studio, les utilisateurs peuvent écrire le code R et en quelques clics, publier sous la forme d’un service web pour les applications et les périphériques tooconsume monde hello.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9ed4f-111">À partir de la production calculatrices simples qui fournissent des fonctionnalités statistique toocreating PRÉDICTEUR sentiment analysis personnalisées d’exploration de données texte, les utilisateurs de R de nouveaux et expérimentés peuvent bénéficier de la facilité hello avec laquelle les utilisateurs d’Azure Machine Learning pour opérationnaliser les R code.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="9ed4f-112">Alors que ces services web pouvant être consommées par les utilisateurs, via une application mobile ou un site Web, le but de hello de ces services web exemples est tooshow comment apprentissage peut mettre R scripts à des fins analytiques et être des services web toocreate utilisé sur en haut du code R.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="9ed4f-113">Chaque exemple inclut un exemple C# de consommation du service web.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-113">Each example includes a C# example for web service consumption.</span></span>

![Diagramme du code R dans Azure Machine Learning : solutions R toohello publié Azure Marketplace ou propriétaires.][1]

<span data-ttu-id="9ed4f-115">Envisagez de hello les scénarios suivants.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="9ed4f-116">Scénario 1 : modèle générique</span><span class="sxs-lookup"><span data-stu-id="9ed4f-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="9ed4f-117">Un utilisateur travaille avec un modèle générique qui peut être des données tooa appliquée du nouvel utilisateur, par exemple une prévision de base de données de série chronologique ou d’une méthode personnalisée de R avec analytique avancée.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="9ed4f-118">Cet utilisateur publie hello de modèle comme un service web pour d’autres tooconsume avec leurs données.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="9ed4f-119">Classifieur binaire</span><span class="sxs-lookup"><span data-stu-id="9ed4f-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="9ed4f-120">Modèle de cluster</span><span class="sxs-lookup"><span data-stu-id="9ed4f-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="9ed4f-121">Régression linéaire multivariable</span><span class="sxs-lookup"><span data-stu-id="9ed4f-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="9ed4f-122">Prévisions : lissage exponentiel</span><span class="sxs-lookup"><span data-stu-id="9ed4f-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="9ed4f-123">Prévisions ETS + STL</span><span class="sxs-lookup"><span data-stu-id="9ed4f-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="9ed4f-124">Prévisions - Modèle ARIMA (Autoregressive Integrated Moving Average, moyenne mobile intégrée auto-régressive)</span><span class="sxs-lookup"><span data-stu-id="9ed4f-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="9ed4f-125">Analyse de survie</span><span class="sxs-lookup"><span data-stu-id="9ed4f-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="9ed4f-126">Scénario 2 : modèle formé : données spécifiques</span><span class="sxs-lookup"><span data-stu-id="9ed4f-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="9ed4f-127">Un utilisateur a des données qui fournissent des prédictions utiles via le code R, telle qu’un grand échantillon des questionnaires de personnalité en cluster à travers le type de personnalité k-means algorithme toopredict hello d’un utilisateur, ou l’intégrité enquête de données qui peuvent être utilisé toopredict d’un individu risque au cancer du poumon avec un package d’analyse R de survie.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="9ed4f-128">utilisateur de Hello publie des données de hello via un service web qui prédit les résultats d’un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="9ed4f-129">Scénario 3 : modèle formé : données génériques</span><span class="sxs-lookup"><span data-stu-id="9ed4f-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="9ed4f-130">Un utilisateur a des données génériques (par exemple, un corpus de texte) qui permet une toobe de service web créé et appliqué générique sur différents types de scénarios et cas d’usage.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="9ed4f-131">Analyse de sentiments basée sur un lexique</span><span class="sxs-lookup"><span data-stu-id="9ed4f-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="9ed4f-132">Scénario 4 : calculatrice avancée</span><span class="sxs-lookup"><span data-stu-id="9ed4f-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="9ed4f-133">Un utilisateur fournit des calculs avancés ou simulations qui ne nécessitent pas l’ajustement des données d’un utilisateur toohello modèle ni modèle formé.</span><span class="sxs-lookup"><span data-stu-id="9ed4f-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="9ed4f-134">Test de différence des proportions</span><span class="sxs-lookup"><span data-stu-id="9ed4f-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="9ed4f-135">Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="9ed4f-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="9ed4f-136">Suite de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="9ed4f-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="9ed4f-137">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="9ed4f-137">FAQ</span></span>
<span data-ttu-id="9ed4f-138">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9ed4f-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



