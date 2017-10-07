---
title: aaaOptimize vos algorithmes dans Azure Machine Learning | Documents Microsoft
description: "Explique comment le paramètre optimal de hello toochoose définie un algorithme dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Choisissez des paramètres toooptimize vos algorithmes dans Azure Machine Learning
Cette rubrique décrit le hyperparameter de droite toochoose hello un algorithme dans Azure Machine Learning. La plupart des algorithmes d’apprentissage automatique ont tooset de paramètres. Lorsque vous l’apprentissage d’un modèle, vous devez tooprovide valeurs pour ces paramètres. l’efficacité de Hello du modèle formé de hello dépend des paramètres de modèle hello que vous choisissez. processus de recherche de jeu optimal de hello de paramètres Hello est connu en tant que *sélection de modèle*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Il existe de sélection de modèle de différentes manières toodo. Dans l’apprentissage, la validation croisée est une des méthodes hello plus largement utilisé pour la sélection de modèle, et il est le mécanisme de sélection de modèle par défaut hello dans Azure Machine Learning. Comme les langages R et Python sont pris en charge par Azure Machine Learning, vous pouvez toujours implémenter votre propre mécanisme de sélection de modèle, via l’un ou l’autre de ces langages.

Il existe quatre étapes dans le processus de hello de trouver le meilleur jeu de paramètres hello :

1. **Définir l’espace du paramètre hello**: pour l’algorithme hello d’abord déterminer les valeurs de paramètre exacte hello souhaité tooconsider.
2. **Définir les paramètres de validation croisée hello**: décidez comment toochoose la validation croisée est prise en charge pour le jeu de données hello.
3. **Définir la métrique de hello**: décidez quels toouse métrique pour déterminer hello meilleur ensemble de paramètres, tels que de précision, quadratique moyenne racine f-score, la précision, rappel ou erreur.
4. **L’apprentissage, évaluer et comparer**: pour chaque combinaison unique de valeurs de paramètre hello, la validation croisée est effectuée par et en fonction de métrique d’erreur hello que vous définissez. Après l’évaluation et la comparaison, vous pouvez choisir le modèle de meilleures performances de hello.

Hello suivant image illustre montre comment cela peut être effectuée dans Azure Machine Learning.

![Trouver hello meilleur jeu de paramètres](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Définir l’espace du paramètre hello
Vous pouvez définir le paramètre hello défini à l’étape de l’initialisation de modèle hello. volet des paramètres de tous les algorithmes d’apprentissage automatique Hello comporte deux modes de formateur : *seul paramètre* et *plage de paramètres*. Choisissez le mode Plage de paramètres. En mode Plage de paramètres, vous pouvez entrer plusieurs valeurs pour chaque paramètre. Vous pouvez entrer des valeurs séparées par des virgules dans la zone de texte hello.

![Arbre de décision optimisé à deux classes, paramètre unique](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 Ou bien, vous pouvez définir des points de hello minimale et maximale de la grille de hello et du nombre total de hello de toobe points généré avec **utiliser le Générateur de plage**. Par défaut, les valeurs de paramètre hello sont générés sur une échelle linéaire. Toutefois, si **échelle logarithmique** est activée, les valeurs hello sont générés dans l’échelle de journal hello (rapport entre des points adjacents hello hello est constante au lieu de leur différence). Pour les paramètres entiers, vous pouvez définir une plage à l’aide d’un trait d’union. Par exemple, « 1-10 » signifie que tous les entiers compris entre 1 et 10 (tous deux inclus) forment le jeu de paramètres hello. Un mode mixte est également pris en charge. Par exemple, hello jeu de paramètres « 1-10, 20, 50 « inclurait entiers de 1 à 10, 20 et 50.

![Arbre de décision optimisé à deux classes, plage de paramètres](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Définir les plis de validation croisée
Hello [Partition and Sample] [ partition-and-sample] module peut être utilisé toorandomly affecter plis toohello données. Bonjour suivant l’exemple de configuration pour le module de hello, nous définir cinq plis et affecter aléatoirement les instances d’exemple toohello numéros un pli.

![Partition et échantillon](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Définir la métrique de hello
Hello [Hyperparamètres de modèle paramétrer] [ tune-model-hyperparameters] module prend en charge pour le choix de manière empirique hello meilleur ensemble de paramètres pour un algorithme spécifique et un jeu de données. En outre tooother des informations concernant la formation hello de modèle, hello **propriétés** volet de ce module inclut métrique hello pour déterminer le jeu de paramètres meilleures hello. Il présente deux listes déroulantes différentes pour les algorithmes de classification et de régression, respectivement. Si l’algorithme hello considérée est un algorithme de classification, la métrique de régression hello est ignorée et vice versa. Dans cet exemple spécifique, les mesures de hello sont **précision**.   

![Paramètres de balayage](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Apprentissage, évaluation et comparaison
Hello même [Hyperparamètres de modèle paramétrer] [ tune-model-hyperparameters] module effectue l’apprentissage de tous les modèles de hello qui correspondent le jeu de paramètres toohello, évalue diverses métriques et crée ensuite hello mieux formé selon hello métrique sélectionnée. Ce module dispose de deux entrées obligatoires :

* apprenant non formé de Hello
* jeu de données Hello

module de Hello possède également un jeu de données facultatif d’entrée. Connectez le jeu de données de hello avec l’entrée de jeu de données obligatoire toohello pli plus d’informations. Si hello dataset ne possède pas toutes les informations de pli, une facteur 10 la validation croisée est exécutée automatiquement par défaut. Si l’affectation de plis hello n’est pas effectuée et un jeu de données de validation est fourni sur le port de jeu de données facultatif hello, puis un mode d’apprentissage et de test est choisi et hello le premier jeu de données est le modèle de hello tootrain utilisés pour chaque combinaison de paramètres.

![Classifieur d’arbre de décision optimisé](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

modèle de Hello est ensuite évaluée sur un jeu de données de validation hello. Hello laissées sur port de sortie de hello module affiche mesures différentes fonctions de valeurs de paramètre. Hello droite port de sortie donne le modèle formé hello qui correspond le modèle de meilleures performances toohello selon toohello choisi métrique (**précision** dans ce cas).  

![Jeu de données de validation](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Vous pouvez voir les paramètres exacts hello choisis en affichant le port de sortie de droite hello. Ce modèle peut être utilisé lors du calcul de la notation d’un ensemble de test ou dans un service web mis en œuvre après l’enregistrement en tant que modèle formé.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
