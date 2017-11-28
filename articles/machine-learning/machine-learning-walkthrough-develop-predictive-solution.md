---
title: "Solution prédictive des risques de crédit avec Machine Learning| Microsoft Docs"
description: "Guide pas à pas détaillé indiquant comment créer une solution d'analyse prédictive pour l'évaluation des risques de crédit dans Azure Machine Learning Studio."
keywords: "risque de crédit, solution d’analyse prédictive, évaluation des risques"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="3b7d1-104">Guide pas à pas : développer une solution d'analyse prédictive pour l'évaluation des risques de crédit dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3b7d1-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="3b7d1-105">Dans cette procédure détaillée, nous étudierons de manière approfondie le processus de développement d’une solution d’analyse prédictive dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="3b7d1-106">Nous allons développer un modèle simple dans Machine Learning Studio, puis le déployer dans le service web Azure Machine Learning, où le modèle peut effectuer des prévisions à l’aide de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="3b7d1-107">Cette procédure détaillée suppose que vous avez utilisé Machine Learning Studio au moins une fois auparavant et que vous comprenez les concepts de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="3b7d1-108">Il ne suppose pas non plus que vous êtes un expert.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="3b7d1-109">Si vous n’avez jamais utilisé **Azure Machine Learning Studio** auparavant, commencez par le didacticiel [Création de votre première expérience de science des données dans Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="3b7d1-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="3b7d1-110">Ce didacticiel vous accompagne lors de votre première utilisation de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="3b7d1-111">Vous y découvrirez les principes fondamentaux de glisser-déplacer des modules vers votre expérience, et comment les connecter, réaliser votre expérience et étudier les résultats.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="3b7d1-112">Un autre outil qui peut être utile pour la prise en main est un diagramme qui donne une vue d’ensemble des fonctionnalités de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="3b7d1-113">Vous pouvez télécharger le document et l’imprimer ici : [Diagramme de vue d’ensemble des fonctionnalités d’Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="3b7d1-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="3b7d1-114">Si vous êtes novice dans le domaine de l’apprentissage automatique en général, voici une série de vidéos qui peuvent s’avérer utiles pour vous.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="3b7d1-115">Il s’agit de la [Science des données pour les débutants](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md), une excellente introduction à l’apprentissage automatique, qui utilise le langage et les concepts courants.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="3b7d1-116">Le problème</span><span class="sxs-lookup"><span data-stu-id="3b7d1-116">The problem</span></span>

<span data-ttu-id="3b7d1-117">Supposons que vous deviez prédire le risque lié à l'octroi d'un crédit à un individu sur la base des informations fournies lors d'une demande de crédit.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="3b7d1-118">L’évaluation du risque de crédit est un problème complexe, mais nous pouvons le simplifier un peu pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="3b7d1-119">Nous allons l’utiliser comme exemple de création d’une solution d’analyse prédictive à l’aide de Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="3b7d1-120">Pour ce faire, nous utilisons Machine Learning Studio et un service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="3b7d1-121">La solution</span><span class="sxs-lookup"><span data-stu-id="3b7d1-121">The solution</span></span>

<span data-ttu-id="3b7d1-122">Dans cette procédure pas à pas détaillée, nous démarrons avec des données de risque crédit disponibles publiquement, puis développons et formons un modèle prédictif basé sur ces données.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="3b7d1-123">Nous déployons ensuite le modèle comme un service web afin qu’il puisse être utilisé par d’autres pour l’évaluation du risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="3b7d1-124">Pour créer cette solution d'évaluation des risques de crédit, nous suivons ces étapes :</span><span class="sxs-lookup"><span data-stu-id="3b7d1-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="3b7d1-125">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3b7d1-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="3b7d1-126">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="3b7d1-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="3b7d1-127">Création d'une expérience</span><span class="sxs-lookup"><span data-stu-id="3b7d1-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="3b7d1-128">Former et évaluer les modèles</span><span class="sxs-lookup"><span data-stu-id="3b7d1-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="3b7d1-129">Déployer le service web</span><span class="sxs-lookup"><span data-stu-id="3b7d1-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="3b7d1-130">Accéder au service web</span><span class="sxs-lookup"><span data-stu-id="3b7d1-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="3b7d1-131">Vous pouvez obtenir une copie de travail de l’expérience que nous développons lors de cette procédure pas à pas dans la [galerie Cortana Intelligence](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3b7d1-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3b7d1-132">Accédez à **[Procédure pas à pas - Prédiction du risque de crédit](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** et cliquez sur **Ouvrir dans Studio** pour télécharger une copie de l’expérience dans votre espace de travail Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3b7d1-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="3b7d1-133">Cette procédure pas à pas est basée sur une version simplifiée de l’exemple d’expérience [Classification binaire : prédiction du risque de crédit](http://go.microsoft.com/fwlink/?LinkID=525270) également disponible dans la [Galerie](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="3b7d1-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
