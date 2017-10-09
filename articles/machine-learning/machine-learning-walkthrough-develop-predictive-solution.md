---
title: "solution prédictive aaaA risque de crédit avec Machine Learning | Documents Microsoft"
description: "La procédure détaillée montrant comment toocreate une solution prédictive analytique pour crédit l’évaluation des risques dans Azure Machine Learning Studio."
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
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="5a3e9-104">Guide pas à pas : développer une solution d'analyse prédictive pour l'évaluation des risques de crédit dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a3e9-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="5a3e9-105">Dans cette procédure pas à pas, nous examiner une étendue processus hello du développement d’une solution prédictive analytique dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="5a3e9-106">Nous développer un modèle simple dans Machine Learning Studio, puis la déployer en tant qu’un service web d’Azure Machine Learning où les modèle de hello peut élaborer des prédictions à l’aide de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="5a3e9-107">Cette procédure détaillée suppose que vous avez utilisé Machine Learning Studio au moins une fois auparavant et que vous comprenez les concepts de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="5a3e9-108">Il ne suppose pas non plus que vous êtes un expert.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="5a3e9-109">Si vous n’avez jamais utilisé **Azure Machine Learning Studio** avant, vous souhaiterez peut-être toostart avec le didacticiel de hello, [créer votre première pour la science des données faire des essais dans Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="5a3e9-110">Ce didacticiel vous guide Machine Learning Studio pour hello première fois.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="5a3e9-111">Il vous montre hello principes de base des modules comment toodrag glisser-déplacer sur votre expérience, connectez-les, exécutez hello expérience et examiner les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="5a3e9-112">Un autre outil qui peut être utile pour la prise en main est un diagramme qui donne une vue d’ensemble des fonctionnalités de hello de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="5a3e9-113">Vous pouvez télécharger le document et l’imprimer ici : [Diagramme de vue d’ensemble des fonctionnalités d’Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="5a3e9-114">Si vous êtes de nouveau champ toohello d’apprentissage en général, il est une série de vidéos qui peut être utile tooyou.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="5a3e9-115">Il est appelé [Science des données pour les débutants](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) et il peut vous donner une formation de toomachine bonne introduction à l’aide de la langue de tous les jours et les concepts.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="5a3e9-116">problème de Hello</span><span class="sxs-lookup"><span data-stu-id="5a3e9-116">hello problem</span></span>

<span data-ttu-id="5a3e9-117">Supposons que vous avez besoin de toopredict risque de crédit d’un individu en fonction des informations de hello qu'ils a donné sur une application de crédit.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="5a3e9-118">L’évaluation du risque de crédit est un problème complexe, mais nous pouvons le simplifier un peu pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="5a3e9-119">Nous allons l’utiliser comme exemple de création d’une solution d’analyse prédictive à l’aide de Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="5a3e9-120">toodo, nous utilisons Azure Machine Learning Studio et le service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="5a3e9-121">solution de Hello</span><span class="sxs-lookup"><span data-stu-id="5a3e9-121">hello solution</span></span>

<span data-ttu-id="5a3e9-122">Dans cette procédure pas à pas détaillée, nous démarrons avec des données de risque crédit disponibles publiquement, puis développons et formons un modèle prédictif basé sur ces données.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="5a3e9-123">Nous ensuite déployer le modèle de hello comme un service web afin qu’il peut être utilisé par d’autres pour l’évaluation des risques de crédit.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="5a3e9-124">toocreate cette solution d’évaluation des risques crédit, nous procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a3e9-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="5a3e9-125">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a3e9-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="5a3e9-126">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="5a3e9-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="5a3e9-127">Création d'une expérience</span><span class="sxs-lookup"><span data-stu-id="5a3e9-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="5a3e9-128">L’apprentissage et évaluer des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="5a3e9-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="5a3e9-129">Déployer le service web de hello</span><span class="sxs-lookup"><span data-stu-id="5a3e9-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="5a3e9-130">Service d’accès hello web</span><span class="sxs-lookup"><span data-stu-id="5a3e9-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="5a3e9-131">Vous trouverez une copie de travail d’expérimentation hello que nous développez dans cette procédure pas à pas Bonjour [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5a3e9-132">Accédez trop**[procédure pas à pas : prédiction de risque de crédit](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  et cliquez sur **ouvrir dans Studio** toodownload une copie de l’expérience hello dans votre espace de travail Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="5a3e9-133">Cette procédure pas à pas est basée sur une version simplifiée de l’expérience exemple hello, [Classification binaire : prédiction de risque de crédit](http://go.microsoft.com/fwlink/?LinkID=525270), également disponible dans hello [galerie](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
