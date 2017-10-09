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
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Guide pas à pas : développer une solution d'analyse prédictive pour l'évaluation des risques de crédit dans Azure Machine Learning

Dans cette procédure pas à pas, nous examiner une étendue processus hello du développement d’une solution prédictive analytique dans Machine Learning Studio. Nous développer un modèle simple dans Machine Learning Studio, puis la déployer en tant qu’un service web d’Azure Machine Learning où les modèle de hello peut élaborer des prédictions à l’aide de nouvelles données. 

Cette procédure détaillée suppose que vous avez utilisé Machine Learning Studio au moins une fois auparavant et que vous comprenez les concepts de Machine Learning. Il ne suppose pas non plus que vous êtes un expert.

Si vous n’avez jamais utilisé **Azure Machine Learning Studio** avant, vous souhaiterez peut-être toostart avec le didacticiel de hello, [créer votre première pour la science des données faire des essais dans Azure Machine Learning Studio](machine-learning-create-experiment.md). Ce didacticiel vous guide Machine Learning Studio pour hello première fois. Il vous montre hello principes de base des modules comment toodrag glisser-déplacer sur votre expérience, connectez-les, exécutez hello expérience et examiner les résultats de hello. Un autre outil qui peut être utile pour la prise en main est un diagramme qui donne une vue d’ensemble des fonctionnalités de hello de Machine Learning Studio. Vous pouvez télécharger le document et l’imprimer ici : [Diagramme de vue d’ensemble des fonctionnalités d’Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
 
Si vous êtes de nouveau champ toohello d’apprentissage en général, il est une série de vidéos qui peut être utile tooyou. Il est appelé [Science des données pour les débutants](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) et il peut vous donner une formation de toomachine bonne introduction à l’aide de la langue de tous les jours et les concepts.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>problème de Hello

Supposons que vous avez besoin de toopredict risque de crédit d’un individu en fonction des informations de hello qu'ils a donné sur une application de crédit.  

L’évaluation du risque de crédit est un problème complexe, mais nous pouvons le simplifier un peu pour cette procédure pas à pas. Nous allons l’utiliser comme exemple de création d’une solution d’analyse prédictive à l’aide de Microsoft Azure Machine Learning. toodo, nous utilisons Azure Machine Learning Studio et le service web Machine Learning.  

## <a name="hello-solution"></a>solution de Hello

Dans cette procédure pas à pas détaillée, nous démarrons avec des données de risque crédit disponibles publiquement, puis développons et formons un modèle prédictif basé sur ces données. Nous ensuite déployer le modèle de hello comme un service web afin qu’il peut être utilisé par d’autres pour l’évaluation des risques de crédit.

toocreate cette solution d’évaluation des risques crédit, nous procédez comme suit :  

1. [Créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Télécharger des données existantes](machine-learning-walkthrough-2-upload-data.md)
3. [Création d'une expérience](machine-learning-walkthrough-3-create-new-experiment.md)
4. [L’apprentissage et évaluer des modèles de hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Déployer le service web de hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Service d’accès hello web](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> Vous trouverez une copie de travail d’expérimentation hello que nous développez dans cette procédure pas à pas Bonjour [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com). Accédez trop**[procédure pas à pas : prédiction de risque de crédit](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  et cliquez sur **ouvrir dans Studio** toodownload une copie de l’expérience hello dans votre espace de travail Machine Learning Studio.
> 
> Cette procédure pas à pas est basée sur une version simplifiée de l’expérience exemple hello, [Classification binaire : prédiction de risque de crédit](http://go.microsoft.com/fwlink/?LinkID=525270), également disponible dans hello [galerie](http://gallery.cortanaintelligence.com/).
