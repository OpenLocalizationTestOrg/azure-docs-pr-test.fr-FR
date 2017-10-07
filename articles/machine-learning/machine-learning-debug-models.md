---
title: "aaaDebug votre modèle dans Azure Machine Learning | Documents Microsoft"
description: "Comment les erreurs de toodebug générées par le modèle d’apprentissage et de modèle de Score modules dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="6ed16-103">Déboguer votre modèle dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6ed16-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="6ed16-104">Cet article explique les raisons possibles hello pourquoi de hello après deux défaillances peuvent être détectés lors de l’exécution d’un modèle :</span><span class="sxs-lookup"><span data-stu-id="6ed16-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="6ed16-105">Hello [Train Model] [ train-model] module génère une erreur</span><span class="sxs-lookup"><span data-stu-id="6ed16-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="6ed16-106">Hello [Score Model] [ score-model] module génère des résultats incorrects</span><span class="sxs-lookup"><span data-stu-id="6ed16-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="6ed16-107">le module Former le modèle génère une erreur ;</span><span class="sxs-lookup"><span data-stu-id="6ed16-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="6ed16-109">Hello [Train Model] [ train-model] Module attend deux entrées :</span><span class="sxs-lookup"><span data-stu-id="6ed16-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="6ed16-110">type de Hello du modèle d’apprentissage automatique à partir de la collection hello des modèles fournis par Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6ed16-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="6ed16-111">données d’apprentissage avec une colonne d’étiquette spécifiée qui spécifie Hello hello toopredict variable (hello autres colonnes sont considérées comme des fonctionnalités de toobe).</span><span class="sxs-lookup"><span data-stu-id="6ed16-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="6ed16-112">Ce module peut engendrer une erreur Bonjour suivant cas :</span><span class="sxs-lookup"><span data-stu-id="6ed16-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="6ed16-113">colonne d’étiquette Hello est spécifié correctement.</span><span class="sxs-lookup"><span data-stu-id="6ed16-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="6ed16-114">Cela peut se produire si plusieurs colonnes est sélectionné en tant qu’étiquette de hello ou un index de colonne incorrect est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6ed16-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="6ed16-115">Par exemple, second cas de hello s’applique également si un index de colonne de 30 est utilisé avec un jeu de données d’entrée qui comporte les colonnes que 25.</span><span class="sxs-lookup"><span data-stu-id="6ed16-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="6ed16-116">Hello dataset ne contient pas toutes les colonnes de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6ed16-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="6ed16-117">Par exemple, si le jeu de données d’entrée hello n'a qu’une seule colonne, qui est marquée en tant que colonne d’étiquette hello, il ne serait aucuns fonctionnalités avec le modèle de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="6ed16-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="6ed16-118">Dans ce cas, hello [Train Model] [ train-model] module génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="6ed16-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="6ed16-119">Hello le dataset d’entrée (fonctionnalités ou étiquette) contient l’infini comme valeur.</span><span class="sxs-lookup"><span data-stu-id="6ed16-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="6ed16-120">Le module Noter le modèle produit des résultats incorrects</span><span class="sxs-lookup"><span data-stu-id="6ed16-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="6ed16-122">Dans un classique d’apprentissage/test expérience d’apprentissage supervisé, hello [données fractionnées] [ split] module divise le jeu de données d’origine hello en deux parties : une partie est le modèle de hello tootrain utilisé et une partie est utilisée. tooscore si fonctionne bien formé hello.</span><span class="sxs-lookup"><span data-stu-id="6ed16-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="6ed16-123">modèle formé de Hello est utilisé tooscore hello des données de test, après laquelle les résultats hello sont évaluées toodetermine hello analyse de précision du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="6ed16-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="6ed16-124">Hello [Score Model] [ score-model] module requiert deux entrées :</span><span class="sxs-lookup"><span data-stu-id="6ed16-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="6ed16-125">Une sortie de modèle formé à partir de hello [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="6ed16-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="6ed16-126">Un jeu de données score qui diffère de jeu de données hello utilisé modèle de hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="6ed16-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="6ed16-127">Il s’agit de possible même si l’expérience de hello réussit, hello [Score Model] [ score-model] module génère des résultats incorrects.</span><span class="sxs-lookup"><span data-stu-id="6ed16-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="6ed16-128">Plusieurs scénarios peuvent provoquer cette toohappen :</span><span class="sxs-lookup"><span data-stu-id="6ed16-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="6ed16-129">Si hello spécifié étiquette est catégorique et un modèle de régression est formé sur les données de salutation, une sortie incorrecte serait produite par hello [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="6ed16-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="6ed16-130">Ceci est dû au fait que la régression requiert une variable dépendante continue.</span><span class="sxs-lookup"><span data-stu-id="6ed16-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="6ed16-131">Dans ce cas, il serait plus adapté toouse un modèle de classification.</span><span class="sxs-lookup"><span data-stu-id="6ed16-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="6ed16-132">De même, si un modèle de classification est formé sur un jeu de données ayant des nombres à virgule flottante dans la colonne d’étiquette hello, elle peut produire des résultats indésirables.</span><span class="sxs-lookup"><span data-stu-id="6ed16-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="6ed16-133">Ceci s’explique par le fait que la classification requiert une variable dépendante discontinue qui autorise uniquement les valeurs couvrant un ensemble de classes fini et généralement plutôt restreint.</span><span class="sxs-lookup"><span data-stu-id="6ed16-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="6ed16-134">Si hello calcul du score du jeu de données ne contient pas tous les modèles de hello tootrain hello fonctionnalités utilisées, hello [Score Model] [ score-model] génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="6ed16-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="6ed16-135">Si une ligne hello calcul du score du jeu de données contient une valeur manquante ou une valeur infinie pour une de ses fonctionnalités, hello [Score Model] [ score-model] ne produira pas toute ligne toothat correspondante de sortie.</span><span class="sxs-lookup"><span data-stu-id="6ed16-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="6ed16-136">Hello [Score Model] [ score-model] peut produire des sorties identiques pour toutes les lignes de hello calcul du score du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="6ed16-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="6ed16-137">Cela peut se produire, par exemple, lors de la tentative de classification à l’aide de forêts décisionnelles si le nombre minimal de hello d’échantillons par nœud terminal est choisi toobe plus de hello nombre d’exemples d’apprentissage disponibles.</span><span class="sxs-lookup"><span data-stu-id="6ed16-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

