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
# <a name="debug-your-model-in-azure-machine-learning"></a>Déboguer votre modèle dans Azure Machine Learning

Cet article explique les raisons possibles hello pourquoi de hello après deux défaillances peuvent être détectés lors de l’exécution d’un modèle :

* Hello [Train Model] [ train-model] module génère une erreur 
* Hello [Score Model] [ score-model] module génère des résultats incorrects 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>le module Former le modèle génère une erreur ;

![image1](./media/machine-learning-debug-models/train_model-1.png)

Hello [Train Model] [ train-model] Module attend deux entrées :

1. type de Hello du modèle d’apprentissage automatique à partir de la collection hello des modèles fournis par Azure Machine Learning.
2. données d’apprentissage avec une colonne d’étiquette spécifiée qui spécifie Hello hello toopredict variable (hello autres colonnes sont considérées comme des fonctionnalités de toobe).

Ce module peut engendrer une erreur Bonjour suivant cas :

1. colonne d’étiquette Hello est spécifié correctement. Cela peut se produire si plusieurs colonnes est sélectionné en tant qu’étiquette de hello ou un index de colonne incorrect est sélectionné. Par exemple, second cas de hello s’applique également si un index de colonne de 30 est utilisé avec un jeu de données d’entrée qui comporte les colonnes que 25.

2. Hello dataset ne contient pas toutes les colonnes de fonctionnalité. Par exemple, si le jeu de données d’entrée hello n'a qu’une seule colonne, qui est marquée en tant que colonne d’étiquette hello, il ne serait aucuns fonctionnalités avec le modèle de hello toobuild. Dans ce cas, hello [Train Model] [ train-model] module génère une erreur.

3. Hello le dataset d’entrée (fonctionnalités ou étiquette) contient l’infini comme valeur.

## <a name="score-model-module-produces-incorrect-results"></a>Le module Noter le modèle produit des résultats incorrects

![image2](./media/machine-learning-debug-models/train_test-2.png)

Dans un classique d’apprentissage/test expérience d’apprentissage supervisé, hello [données fractionnées] [ split] module divise le jeu de données d’origine hello en deux parties : une partie est le modèle de hello tootrain utilisé et une partie est utilisée. tooscore si fonctionne bien formé hello. modèle formé de Hello est utilisé tooscore hello des données de test, après laquelle les résultats hello sont évaluées toodetermine hello analyse de précision du modèle de hello.

Hello [Score Model] [ score-model] module requiert deux entrées :

1. Une sortie de modèle formé à partir de hello [Train Model] [ train-model] module.
2. Un jeu de données score qui diffère de jeu de données hello utilisé modèle de hello tootrain.

Il s’agit de possible même si l’expérience de hello réussit, hello [Score Model] [ score-model] module génère des résultats incorrects. Plusieurs scénarios peuvent provoquer cette toohappen :

1. Si hello spécifié étiquette est catégorique et un modèle de régression est formé sur les données de salutation, une sortie incorrecte serait produite par hello [Score Model] [ score-model] module. Ceci est dû au fait que la régression requiert une variable dépendante continue. Dans ce cas, il serait plus adapté toouse un modèle de classification. 

2. De même, si un modèle de classification est formé sur un jeu de données ayant des nombres à virgule flottante dans la colonne d’étiquette hello, elle peut produire des résultats indésirables. Ceci s’explique par le fait que la classification requiert une variable dépendante discontinue qui autorise uniquement les valeurs couvrant un ensemble de classes fini et généralement plutôt restreint.

3. Si hello calcul du score du jeu de données ne contient pas tous les modèles de hello tootrain hello fonctionnalités utilisées, hello [Score Model] [ score-model] génère une erreur.

4. Si une ligne hello calcul du score du jeu de données contient une valeur manquante ou une valeur infinie pour une de ses fonctionnalités, hello [Score Model] [ score-model] ne produira pas toute ligne toothat correspondante de sortie.

5. Hello [Score Model] [ score-model] peut produire des sorties identiques pour toutes les lignes de hello calcul du score du jeu de données. Cela peut se produire, par exemple, lors de la tentative de classification à l’aide de forêts décisionnelles si le nombre minimal de hello d’échantillons par nœud terminal est choisi toobe plus de hello nombre d’exemples d’apprentissage disponibles.

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

