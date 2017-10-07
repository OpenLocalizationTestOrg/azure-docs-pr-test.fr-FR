---
title: "performances du modèle aaaEvaluate dans l’apprentissage | Documents Microsoft"
description: "Explique comment tooevaluate modèle de performances dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Comment tooevaluate modèle de performances dans Azure Machine Learning
Cet article explique comment tooevaluate hello des performances d’un modèle dans Azure Machine Learning Studio et fournit une brève explication de métriques hello disponibles pour cette tâche. Il vous présente trois scénarios d’apprentissage supervisé courants : 

* régression ;
* classification binaire ; 
* classification multiclasse.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

L’évaluation des performances hello d’un modèle est une des étapes de base hello dans le processus de science des données hello. Il indique comment réussie hello score (prévisions) d’un jeu de données a été par un modèle formé. 

Azure Machine Learning prend en charge l’évaluation des modèles via deux de ses principaux modules d’apprentissage automatique : [Évaluer le modèle][evaluate-model] et [Effectuer la validation croisée du modèle][cross-validate-model]. Ces modules permettent toosee le fonctionnement de votre modèle en termes d’un nombre de mesures qui sont couramment utilisés dans les statistiques et l’apprentissage.

## <a name="evaluation-vs-cross-validation"></a>Évaluation et validation croisée
Évaluation et validation croisée sont les performances de hello toomeasure méthodes standard de votre modèle. Elles génèrent toutes deux des métriques d’évaluation que vous pouvez inspecter ou comparer avec les métriques d’autres modèles.

[Évaluation du modèle] [ evaluate-model] attend un jeu de données au score calculé en tant qu’entrée (ou vous souhaitez que les performances de hello toocompare 2 modèles différents dans le cas 2). Cela signifie que vous avez tootrain votre modèle à l’aide de hello [Train Model] [ train-model] module et apporter des prédictions sur des dataset à l’aide de hello [Score Model] [ score-model] module, avant de pouvoir évaluer les résultats hello. Hello évaluation est basée sur hello transformée étiquettes/probabilités, ainsi que les étiquettes true hello, qui sont tous des sorties par hello [Score Model] [ score-model] module.

Vous pouvez également utiliser la validation croisée tooperform un nombre d’évaluer train-score opérations (10 plis) automatiquement sur des sous-ensembles de données d’entrée de hello. les données d’entrée Hello sont divisées en 10 parties, où un est réservé pour le test et hello autres 9 pour l’apprentissage. Ce processus se répète 10 fois et les mesures d’évaluation de hello moyenne sont calculées. Cela permet de déterminer comment un modèle serait généraliser toonew de jeux de données. Hello [Cross-Validate Model] [ cross-validate-model] module prend dans un modèle non formé et certains étiqueté des résultats d’évaluation de hello du jeu de données et les sorties de chacun des hello 10 plis, en outre toohello moyenne des résultats.

Bonjour les sections suivantes, nous allons en générer des modèles de régression et classification simples et évaluer leurs performances, à l’aide de deux hello [modèle Evaluate] [ evaluate-model] et hello [Cross-Validate Modèle] [ cross-validate-model] modules.

## <a name="evaluating-a-regression-model"></a>Évaluation d’un modèle de régression
Supposons que nous souhaitons toopredict prix d’une voiture à l’aide de certaines fonctionnalités telles que les dimensions, la puissance, les spécifications de moteur et ainsi de suite. Il s’agit d’un problème de régression classiques, où hello variable cible (*prix*) est une valeur numérique continue. Nous pouvons faire tenir un modèle de régression linéaire simple que, compte tenu de la fonctionnalité de hello valeurs d’une voiture, certains peut prédire prix hello de cette voiture. Ce modèle de régression utilisable tooscore hello même dataset nous formés sur. Une fois que nous avons hello prédites prix pour toutes les voitures de hello, nous pouvons évaluer les performances de hello du modèle de hello en examinant la quantité des prédictions de hello écartent pratiqués hello en moyenne. tooillustrate, nous utilisons hello *jeu de données (Raw) de données de prix Automobile* disponibles dans hello **jeux de données enregistrés** section dans Azure Machine Learning Studio.

### <a name="creating-hello-experiment"></a>Hello expérience de création
Ajoutez hello suivant modules tooyour espace de travail Azure Machine Learning Studio :

* Données sur le prix des véhicules automobiles (brutes)
* [Régression linéaire][linear-regression]
* [Former le modèle][train-model]
* [Noter le modèle][score-model]
* [Évaluer le modèle][evaluate-model]

Connecter les ports de hello comme indiqué ci-dessous dans la Figure 1 et la colonne d’étiquette ensemble hello Hello [Train Model] [ train-model] module trop*prix*.

![Évaluation d’un modèle de régression](media/machine-learning-evaluate-model-performance/1.png)

Figure 1. évaluation d’un modèle de régression

### <a name="inspecting-hello-evaluation-results"></a>Inspection des résultats de l’évaluation hello
Après l’expérience hello en cours d’exécution, vous pouvez cliquer sur le port de sortie hello Hello [modèle Evaluate] [ evaluate-model] module et sélectionnez *visualiser* résultats de l’évaluation toosee hello. Hello des mesures d’évaluation disponibles pour les modèles de régression sont : *erreur d’absolue moyenne*, *erreur d’absolue moyenne racine*, *erreur absolue Relative*,  *Erreur de quadratique relative*et hello *Coefficient de détermination*.

terme Hello « erreur » représente la différence de hello hello valeur prédite et la valeur true hello. valeur absolue de Hello ou hello carrée de cette différence sont hello généralement calculées toocapture total magnitude d’erreur sur toutes les instances, en tant que différence hello entre hello prédite et la valeur true peut être négative dans certains cas. mesures d’erreur Hello mesurent les performances de prédictive hello d’un modèle de régression en termes d’écart hello de prédictions à partir des valeurs true de hello. Les valeurs d’erreur inférieure signifient modèle de hello est plus précis dans l’élaboration de prédictions. Une métrique de l’erreur globale de 0 signifie que le modèle de hello est parfaitement adaptée aux données de salutation.

coefficient Hello de détermination, qui est également appelé R au carré, est également un moyen standard de mesurer la manière dont le modèle de hello mieux aux données de hello. Il peut être interprété comme la proportion de hello de variation expliquée par modèle de hello. Dans ce cas précis, plus la proportion est élevée, meilleur est le résultat, la valeur 1 indiquant une adéquation parfaite.

![Métriques d’évaluation de régression linéaire](media/machine-learning-evaluate-model-performance/2.png)

Figure 2 : métriques d’évaluation de régression linéaire

### <a name="using-cross-validation"></a>Utilisation de la validation croisée
Comme mentionné précédemment, vous pouvez effectuer une formation répétée, hello de score et les évaluations automatiquement à l’aide [Cross-Validate Model] [ cross-validate-model] module. Pour mener à bien cette tâche, vous avez simplement besoin d’un jeu de données, d’un modèle non formé et d’un module [Effectuer la validation croisée][cross-validate-model] du modèle (voir la figure ci-après). Notez que vous devez la colonne d’étiquette tooset hello trop*prix* Bonjour [Cross-Validate Model] [ cross-validate-model] les propriétés du module.

![Validation croisée d’un modèle de régression](media/machine-learning-evaluate-model-performance/3.png)

Figure 3. validation croisée d’un modèle de régression

Après l’expérience hello en cours d’exécution, vous pouvez inspecter les résultats de l’évaluation hello en cliquant sur le port de sortie de droite hello Hello [Cross-Validate Model] [ cross-validate-model] module. Cela fournit une vue détaillée des métriques de hello pour chaque itération (pli), et hello moyenne des résultats de chacune des métriques de hello (Figure 4).

![Résultats de la validation croisée d’un modèle de régression](media/machine-learning-evaluate-model-performance/4.png)

Figure 4. résultats de la validation croisée d’un modèle de régression

## <a name="evaluating-a-binary-classification-model"></a>Évaluation d’un modèle de classification binaire
Dans un scénario de classification binaire, variable cible de hello a uniquement deux résultats possibles, par exemple : {0, 1} ou {false, true}, {négatif, positif}. Supposons que vous disposez d’un jeu de données d’employés pour adultes avec certains démographiques et variables de l’emploi, et que vous êtes invité à niveau de revenu toopredict hello, une variable binaire avec des valeurs hello {« < = 50 Ko », « > 50K »}. En d’autres termes, classe négatif hello représente employés hello rendre inférieur ou égal too50K par an et hello positif classe représente tous les autres employés. Comme dans le scénario de régression hello, nous serait former un modèle, un score de certaines données et évaluer les résultats hello. Hello sur la principale différence ici est choix hello d’Azure Machine Learning calcule des métriques et des sorties. scénario de prédiction niveau tooillustrate hello revenu, nous allons utiliser hello [adulte](http://archive.ics.uci.edu/ml/datasets/Adult) dataset toocreate un Azure Machine Learning faire des essais et évaluer les performances de hello d’un modèle de régression logistique à deux classes, un fichier binaire couramment utilisé classifieur.

### <a name="creating-hello-experiment"></a>Hello expérience de création
Ajoutez hello suivant modules tooyour espace de travail Azure Machine Learning Studio :

* Jeu de données Adult Census Income Binary Classification
* [Régression logistique à deux classes][two-class-logistic-regression]
* [Former le modèle][train-model]
* [Noter le modèle][score-model]
* [Évaluer le modèle][evaluate-model]

Connecter les ports de hello comme indiqué ci-dessous dans la Figure 5 et la colonne d’étiquette ensemble hello Hello [Train Model] [ train-model] module trop*income*.

![Évaluation d’un modèle de classification binaire](media/machine-learning-evaluate-model-performance/5.png)

Figure 5. évaluation d’un modèle de classification binaire

### <a name="inspecting-hello-evaluation-results"></a>Inspection des résultats de l’évaluation hello
Après l’expérience hello en cours d’exécution, vous pouvez cliquer sur le port de sortie hello Hello [modèle Evaluate] [ evaluate-model] module et sélectionnez *visualiser* toosee les résultats d’évaluation hello (Figure 7). Hello des mesures d’évaluation disponibles pour les modèles de classification binaire sont : *précision*, *précision*, *rappeler*, *F1 Score*, et *AUC*. En outre, le module de hello génère une matrice de confusion montrant le numéro de hello de vrais positifs, faux négatifs, faux positifs et négatifs trues, ainsi que *ROC*, *précision/rappel*et *De courbes d’élévation* courbes.

La précision est simplement les proportion hello d’instances classifiés correctement. Il est généralement hello première mesure qu'examiner lors de l’évaluation d’un classifieur. Toutefois, lorsque les données de test hello sont asymétrique (où la plupart des instances de hello appartenir tooone des classes de hello), ou si vous êtes davantage intéressé performances hello sur l’une des classes de hello, précision ne capture vraiment pas l’efficacité d’un classifieur hello. Dans le scénario de la classification des niveaux de revenu hello, supposons que vous testez sur certaines données, où 99 % des instances de hello représentent les personnes qui sont inférieurs ou égaux too50K par an. Il est possible tooachieve une précision 0,99 prédisant classe hello » < = 50 Ko » pour toutes les instances. classifieur de Hello dans ce cas apparaît toobe effectue un bon de travail global, mais en réalité, il échoue tooclassify des personnes à revenus élevés de hello (hello 1 %) correctement.

Pour cette raison, il est utile toocompute des métriques supplémentaires qui capturent les aspects plus spécifiques de l’évaluation de hello. Avant d’aborder les détails de hello de ces mesures, il est important toounderstand matrice de confusion hello d’une évaluation de la classification binaire. classe Hello étiquettes dans le jeu d’apprentissage hello peuvent prendre uniquement 2 valeurs possibles, ce qui nous généralement reportez-vous tooas positif ou négatif. instances positifs et négatifs Hello un classifieur prédit correctement sont appelés (TP) de vrais positifs et négatifs trues (TN), respectivement. De même, les instances de hello incorrectement classifié sont appelées des faux positifs (FP) et des faux négatifs (FN). matrice de confusion Hello est simplement un tableau montrant le numéro de hello d’instances qui répondent à chacune de ces 4 catégories. Azure Machine Learning décide automatiquement de hello deux classes de jeu de données hello est classe positif hello. Si les étiquettes de classe hello sont des entiers ou les booléen, hello 'true' ou '1' instances étiquetés assignés classe positif hello. Si les étiquettes de hello sont des chaînes, comme dans les cas de hello du jeu de données de revenu hello, les étiquettes de hello sont triées par ordre alphabétique et au niveau du premier hello est choisi classe négatif de hello toobe tandis que hello deuxième niveau est la classe positif hello.

![Matrice de confusion d’une classification binaire](media/machine-learning-evaluate-model-performance/6a.png)

Figure 6. matrice de confusion d’une classification binaire

Revenons un problème de classification toohello income, nous voulons tooask plusieurs questions d’évaluation qui nous aider à comprennent les performances de hello du classifieur hello utilisé. Une question très naturelle est : ' hors des individus hello auxquels hello modèle prédit toobe accumuler > 50 K (TP + FP), combien ont été correctement classées (TP) ? » Peut répondre à cette question en examinant hello **précision** du modèle hello, qui est la proportion de hello de positifs sont classifiés correctement : TP/(TP+FP). Une autre question courante est « en dehors de tous les employés abandonner haute hello dont le revenu > 50 k (TP + FN), le nombre hello classifieur classer correctement (TP) ». Il s’agit réellement hello **rappeler**, ou hello vrai positif : TP/(TP+FN) du classifieur de hello. Vous pouvez remarquer qu’il existe un compromis évident entre la précision et le rappel. Par exemple, étant donné un jeu de données relativement à charge équilibrée, un classifieur qui prédit principalement des instances positifs, aurait un rappel élevé, mais une précision plutôt faible autant d’instances de négatif hello est mal classée entraîne un grand nombre de faux positifs. toosee un traçage de la manière dont ces deux mesures peuvent varier, que vous pouvez cliquer sur la courbe de ' Précision/rappel' hello dans la page de sortie de résultat d’évaluation hello (haut à gauche de la Figure 7).

![Résultats de l’évaluation de la classification binaire](media/machine-learning-evaluate-model-performance/7.png)

Figure 7. résultats de l’évaluation de la classification binaire

Un autre liés métrique est souvent utilisé est hello **F1 Score**, qui prend la précision et rappel en considération. Il est moyenne harmonique de hello de ces métriques de 2 et est calculée en tant que tel : F1 = 2 (Souvenez-vous que la précision x) / (précision + rappel). score de F1 Hello est une version d’évaluation de bonne façon toosummarize hello un nombre unique, mais il est toujours un toolook de bonne pratique à la précision et le rappel toobetter ensemble comprendre comment se comporte un classifieur.

En outre, un peut inspecter taux de positifs true hello et hello taux de faux positifs Bonjour **récepteur d’exploitation caractéristique (ROC)** courbe et hello correspondant **zone sous la courbe (AUC) hello** valeur. Hello proche cette courbe est toohello supérieur coin inférieur gauche, les performances du classifieur du hello de meilleures hello (autrement dit optimisant hello vrai positif taux tout en réduisant le taux de hello faux positifs). Courbes diagonale toohello fermer de hello de traçage, résultat à partir de classifieurs qui ont tendance à des prédictions toomake fermer toorandom estimation.

### <a name="using-cross-validation"></a>Utilisation de la validation croisée
Comme exemple de régression hello, nous pouvons effectuer la validation croisée toorepeatedly train, évaluer et évaluer des sous-ensembles de données de salutation automatiquement. De même, nous pouvons utiliser hello [Cross-Validate Model] [ cross-validate-model] module, un modèle de régression logistique non formé et un jeu de données. colonne d’étiquette Hello doit être défini trop*income* Bonjour [Cross-Validate Model] [ cross-validate-model] les propriétés du module. Une fois que l’expérience de hello en cours d’exécution et en cliquant sur hello droite sortie de hello [Cross-Validate Model] [ cross-validate-model] module, nous pouvons voir les mesures de classification binaire hello les valeurs pour chaque pli, en outre toohello écart type et chaque. 

![Validation croisée d’un modèle de classification binaire](media/machine-learning-evaluate-model-performance/8.png)

Figure 8. validation croisée d’un modèle de classification binaire

![Résultats de la validation croisée d’un classifieur binaire](media/machine-learning-evaluate-model-performance/9.png)

Figure 9. résultats de la validation croisée d’un classifieur binaire

## <a name="evaluating-a-multiclass-classification-model"></a>Évaluation d’un modèle de classification multiclasse
Dans cette expérience, nous allons utiliser hello populaires [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") jeu de données qui contient des instances de 3 différents types (classes) de la plante d’iris hello. Il existe 4 valeurs de caractéristique (longueur et largeur de sépale, longueur et largeur de pétale) pour chaque instance. Dans les expériences précédentes hello nous formés et modèles hello testée à l’aide de hello des jeux de données. Ici, nous allons utiliser hello [données fractionnées] [ split] des sous-ensembles de toocreate 2 de module de données de hello, tout d’abord, effectuer l’apprentissage sur hello, évaluer et évaluer sur hello deuxième. Bonjour données Iris sont publiquement disponible sur hello [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/index.html)et peut être téléchargé à l’aide un [importer des données] [ import-data] module.

### <a name="creating-hello-experiment"></a>Hello expérience de création
Ajoutez hello suivant modules tooyour espace de travail Azure Machine Learning Studio :

* [Importer des données][import-data]
* [Forêt d’arbres de décision multiclasse][multiclass-decision-forest]
* [Fractionner les données][split]
* [Former le modèle][train-model]
* [Noter le modèle][score-model]
* [Évaluer le modèle][evaluate-model]

Connecter les ports de hello comme indiqué ci-dessous dans la Figure 10.

Définir l’index de colonne d’étiquette hello Hello [Train Model] [ train-model] too5 de module. Hello dataset n’a aucune ligne d’en-tête, mais nous savons que cette classe hello étiquettes se trouvent dans hello cinquième colonne.

Cliquez sur hello [importer des données] [ import-data] module et set hello *source de données* propriété trop*URL Web via HTTP*et hello *URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Fraction de hello de jeu de toobe d’instances utilisée pour l’apprentissage Bonjour [données fractionnées] [ split] module (0,7 par exemple).

![évaluation d’un classifieur multiclasse](media/machine-learning-evaluate-model-performance/10.png)

Figure 10. évaluation d’un classifieur multiclasse

### <a name="inspecting-hello-evaluation-results"></a>Inspection des résultats de l’évaluation hello
Exécutez hello expérience, puis cliquez sur le port de sortie hello du [modèle Evaluate][evaluate-model]. Dans ce cas, les résultats de l’évaluation Hello sont présentés sous forme de hello d’une matrice de confusion. matrice de Hello affiche hello réelle par rapport aux instances prévues pour toutes les classes de 3.

![Résultats de l’évaluation de la classification multiclasse](media/machine-learning-evaluate-model-performance/11.png)

Figure 11. résultats de l’évaluation de la classification multiclasse

### <a name="using-cross-validation"></a>Utilisation de la validation croisée
Comme mentionné précédemment, vous pouvez effectuer une formation répétée, hello de score et les évaluations automatiquement à l’aide [Cross-Validate Model] [ cross-validate-model] module. Pour mener à bien cette tâche, vous avez besoin d’un jeu de données, d’un modèle non formé et d’un module [Effectuer la validation croisée du modèle][cross-validate-model] (voir la figure ci-dessous). À nouveau, vous devez colonne d’étiquette tooset hello Hello [Cross-Validate Model] [ cross-validate-model] module (index de colonne 5 dans ce cas). Une fois que l’expérience de hello en cours d’exécution et en cliquant sur la droite hello sortie de hello [Cross-Validate Model][cross-validate-model], vous pouvez inspecter les valeurs de mesure hello pour chaque pli ainsi hello moyenne et l’écart type. métriques de Hello affichés ici sont toohello similaire de hello celles mentionnées dans les cas de classification binaire hello. Toutefois, notez que dans la classification multiclasse, informatique hello vrais positifs/négatifs et faux positifs/négatifs en comptant sur une base par classe, car il n’existe aucune classe global positif ou négatif. Par exemple, lorsque les précision hello informatique ou le rappel Hello 'Iris-setosa' classe, il est supposé qu’il s’agit de classe positif hello et tous les autres comme négative.

![Validation croisée d’un modèle de classification multiclasse](media/machine-learning-evaluate-model-performance/12.png)

Figure 12 : validation croisée d’un modèle de classification multiclasse

![Résultats de la validation croisée d’un modèle de classification multiclasse](media/machine-learning-evaluate-model-performance/13.png)

Figure 13 : résultats de la validation croisée d’un modèle de classification multiclasse

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

