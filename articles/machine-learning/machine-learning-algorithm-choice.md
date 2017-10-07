---
title: "aaaHow toochoose algorithmes d’apprentissage | Documents Microsoft"
description: "Comment toochoose Azure Machine Learning algorithmes d’apprentissage supervisé et non supervisé dans le clustering, classification ou régression d’expériences."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>Comment les algorithmes toochoose pour Microsoft Azure Machine Learning
Hello réponse toohello « ordinateur algorithme d’apprentissage dois-je utiliser ? » est toujours « Cela dépend. ». Il dépend de la nature des données de hello, la qualité et la taille de hello. Il dépend de ce que vous voulez toodo avec les réponses hello. Il dépend comment mathématiques hello d’algorithme de hello a été traduite en instructions pour l’ordinateur que vous utilisez hello. Et cela dépend du temps que vous avez. Même les chercheurs de données hello mieux ne peut pas déterminer quel algorithme effectuera mieux avant d’essayer de les.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>Hello Machine Learning algorithme Cheat Sheet
Hello **Microsoft Azure Machine Learning algorithme Cheat Sheet** vous aide à choisir de droite de hello algorithme d’apprentissage pour vos solutions d’analytique PRÉDICTIFS à partir de la bibliothèque de Microsoft Azure Machine Learning hello des algorithmes de l’ordinateur.
Cet article vous guide toouse il.

> [!NOTE]
> aide-mémoire de toodownload hello et suivez le long de cet article, sont trop[Machine aide-mémoire algorithme d’apprentissage pour Microsoft Azure Machine Learning Studio](machine-learning-algorithm-cheat-sheet.md).
> 
> 

Cette feuille de graphique a une audience très spécifique à l’esprit : un spécialiste des données début avec apprentissage automatique au niveau de l’étudiant du premier cycle, la tentative de toochoose un toostart algorithme avec dans Azure Machine Learning Studio. Cela signifie qu’il comprend certaines généralisations et simplifie trop, mais vous guide en toute sécurité. Cela signifie également qu'il existe un grand nombre d'algorithmes non répertoriés ici. Azure Machine Learning fur tooencompass un ensemble plus complet de méthodes disponibles, nous allons ajouter les.

Ces recommandations sont des commentaires et des conseils compilés d’un grand nombre de scientifiques de données et d’experts en apprentissage automatique. Nous n’a pas été accepté sur tous les éléments, mais j’ai essayé tooharmonize notre avis en un consensus approximative. La plupart des instructions hello de désaccord commence par « Il dépend... »

### <a name="how-toouse-hello-cheat-sheet"></a>La feuille de graphique toouse hello
Lire des étiquettes de chemin d’accès et l’algorithme hello sur le graphique de hello en tant que » pour  *&lt;étiquette de chemin d’accès&gt;*, utilisez  *&lt;algorithme&gt;*. » Par exemple, « Pour *Vitesse*, utilisez la *régression logistique à deux classes* ». Parfois, plusieurs branches sont utiles.
Parfois, aucune n’est parfaite. Ils toobe prévue à la règle de recommandations, par conséquent, ne vous inquiétez est exacte.
J’ai parlé avec des spécialistes des données plusieurs dit que hello uniquement que permettant de rechercher l’algorithme le mieux très hello est tootry d'entre eux.

Voici un exemple de hello [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com/) d’une expérience qui tente de plusieurs algorithmes contre hello les mêmes données et les compare hello résultats : [comparer des classifieurs multi-class : lettre reconnaissance ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> toodownload et imprimer un diagramme qui donne une vue d’ensemble des fonctionnalités de hello de Machine Learning Studio, consultez [diagramme de vue d’ensemble des fonctionnalités d’Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

## <a name="flavors-of-machine-learning"></a>Types d'apprentissage automatique
### <a name="supervised"></a>Supervisé
Les algorithmes d'apprentissage supervisés font des prédictions basées sur un ensemble d'exemples. Par exemple, historique des actions peuvent être propositions toohazard utilisés au prix futurs. Chaque exemple utilisé pour l’apprentissage est étiqueté avec la valeur hello d’intérêt : hello dans ce cas de cotation. Un algorithme d'apprentissage supervisé recherche des modèles dans ces étiquettes de valeur. Il peut utiliser toutes les informations qui peuvent être pertinentes : jour hello de semaine de hello saison de hello, données financières de la société hello, type hello de secteur, présence hello des événements géopolitiques sans interruption, et chaque algorithme de recherche pour différents types de modèles. Une fois que l’algorithme de hello a trouvé hello meilleure manière possible, il utilise que des prédictions toomake de modèle pour sans titre des données de test, les prix de demain.

Il s’agit d’un type d’apprentissage automatique utile et apprécié. Une exception, tous les modules de hello dans Azure Machine Learning surveillées algorithmes d’apprentissage. Plusieurs types spécifiques d'apprentissage supervisé sont représentés dans Azure Machine Learning : la classification, la régression et la détection d’anomalies.

* **Classification**. Lorsque des données de hello sont utilisée toopredict une catégorie, apprentissage supervisé est également appelé classification. Il s’agit de cas de hello lors de l’attribution d’une image en tant qu’image d’un « cat » ou un « dog ». Quand il n’y a que deux choix, on appelle cela la **classification à deux classes** ou **binomiale**. Lorsqu’il existe plusieurs catégories, comme lors de la prédiction gagnant hello de tournoi de printemps NCAA hello, ce problème est connu en tant que **classification multiclasse**.
* **Régression**. Lorsque l’on prédit une valeur, comme le cours de la Bourse, l’apprentissage surveillé est appelé régression.
* **Détection des anomalies**. Hello objectif est parfois tooidentify des points de données sont simplement inhabituels. Dans le cas de la détection des fraudes par exemple, toute dépense très étrange par carte de crédit est suspecte. les variations possibles Hello sont donc de nombreuses et hello donc peu, qu’il se n'agit pas faisable toolearn quelle activité frauduleuse ressemble à des exemples de formation. L’approche utilisée dans la détection d’anomalies est toosimply savoir quelle activité normale ressemble (à l’aide d’un historique non-de transactions frauduleuses) et d’identifier tout ce qui est très différent.

### <a name="unsupervised"></a>Non supervisé
Dans l’apprentissage non supervisé, les points de données n’ont aucune étiquette associée. Au lieu de cela, objectif hello d’une non supervisé l'apprentissage algorithme consiste à organiser les données de salutation d’une manière ou de toodescribe sa structure. Cela peut signifier un regroupement en clusters ou la recherche de différentes manières de visualisation des données complexes afin d’en simplifier l’affichage ou de l’organiser plus efficacement.

### <a name="reinforcement-learning"></a>Apprentissage par renforcement
Dans l’apprentissage de renforcement, algorithme de hello obtient toochoose une action de point de données de réponse tooeach. algorithme d’apprentissage Hello reçoit également un signal de récompense quelques instants plus tard, indiquant la bonne décision de hello a été.
En fonction de cela, algorithme de hello modifie sa stratégie de récompense de commande tooachieve hello la plus élevée. Il n’existe actuellement aucun module d’apprentissage de renforcement dans Azure Machine Learning. Apprentissage de renforcement est courant robotique, où hello ensemble de lectures de capteur à un moment donné dans le temps est un point de données, et algorithme de hello devez choisir l’action de suivant du robot hello. Il est également adapté aux applications d’Internet des objets.

## <a name="considerations-when-choosing-an-algorithm"></a>Considérations lors du choix d'un algorithme
### <a name="accuracy"></a>Précision
Obtenir des réponses plus précis de hello possibles n’est pas toujours nécessaire.
Parfois, en fonction de votre utilisation, une approximation suffit. Si tel est le cas de hello, vous pouvez être en mesure de toocut votre temps de traitement considérablement par conserverez avec plusieurs méthodes approximatives. Un autre avantage des méthodes plus approximatives est qu’elles ont naturellement tendance à éviter [le surajustement](https://youtu.be/DQWI1kvmwRg).

### <a name="training-time"></a>Durée d’apprentissage
Bonjour le nombre de minutes ou heures tootrain nécessaire, qu'un modèle varie beaucoup entre les algorithmes. Le temps d’apprentissage est souvent étroitement lié à la précision, une accompagne généralement hello autres. En outre, certains algorithmes sont plus sensibles toohello nombre de points de données que d’autres.
Lorsque le temps est limité, elles peuvent générer des choix de hello de l’algorithme, en particulier lorsque le jeu de données hello est grande.

### <a name="linearity"></a>Linéarité
Un grand nombre d'algorithmes d'apprentissage automatique utilisent la linéarité. Les algorithmes de classification linéaire supposent que les classes peuvent être séparées par une ligne droite (ou son analogie de dimension supérieure). Ceux-ci incluent la régression logistique et les machines à vecteurs de support (comme implémentées dans Azure Machine Learning).
Les algorithmes de régression linéaire supposent que les tendances des données suivent une ligne droite. Ces hypothèses ne sont pas erronées pour certains problèmes, mais réduisent la précision pour d’autres.

![Frontière de classe non linéaire][1]

***Limite de classe non linéaire*** *: utiliser un algorithme de classification linéaire entraînerait une faible précision*

![Données avec une tendance non linéaire][2]

***Données avec une tendance non linéaire****: une méthode de régression linéaire entraînerait plus d’erreurs*

Malgré leurs limitations, les algorithmes linéaires sont très populaires comme première ligne d'attaque. Ils ont tendance toobe par un algorithme simple et rapide pour l’apprentissage.

### <a name="number-of-parameters"></a>Nombre de paramètres
Les paramètres sont des boutons de hello un chercheur de données obtient tooturn lorsque vous configurez un algorithme. Ils sont des nombres qui affectent le comportement de l’algorithme hello, telles que la tolérance d’erreur ou le nombre d’itérations ou options entre les variantes du comporte de l’algorithme de hello. temps d’apprentissage Hello et l’exactitude de l’algorithme de hello peuvent parfois être des paramètres corrects de hello simplement toogetting très sensibles. En règle générale, les algorithmes avec des paramètres de grands nombres nécessitent hello plus d’essai et erreur toofind une bonne combinaison.

Il existe également un bloc module de [balayage de paramètre](machine-learning-algorithm-parameters-optimize.md) dans Azure Machine Learning qui essaie automatiquement toutes les combinaisons de paramètres à la granularité que vous choisissez. Il s’agit d’un excellent moyen toomake que vous avez fractionné espace du paramètre hello, hello durée tootrain un modèle augmente de façon exponentielle avec un nombre de paramètres hello.

Hello avantage est que de paramètres généralement indique qu’un algorithme a une plus grande souplesse. Il peut souvent obtenir une excellente précision. Fournie que vous trouverez hello bonne combinaison de paramètres.

### <a name="number-of-features"></a>Nombre de fonctionnalités
Pour certains types de données, plusieurs fonctionnalités hello peut être nombre très grand toohello comparés de points de données. C’est souvent hello cas avec génétique ou des données textuelles. Hello grand nombre de fonctionnalités risque de ralentir certains algorithmes d’apprentissage automatique, rendre formation heure unfeasibly long. Machines à vecteurs de support sont particulièrement bien adapté toothis cas (voir ci-dessous).

### <a name="special-cases"></a>Cas particuliers
Certains algorithmes d’apprentissage automatique présumez particulier structure hello des données de salutation ou les résultats de hello souhaité. Si vous pouvez en trouver un qui répond à vos besoins, il peut vous donner des résultats plus pertinents, des prévisions plus précises ou des durées d'apprentissage plus courtes.

| **Algorithme** | **Précision** | **Durée d’apprentissage** | **Linéarité** | **Paramètres** | **Remarques** |
| --- |:---:|:---:|:---:|:---:| --- |
| **Classification double classe.** | | | | | |
| [régression logique](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [forêt de décision](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [jungle de décision](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |Faible encombrement de mémoire |
| [arbre de décision optimisé](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |Encombrement de mémoire important |
| [réseau neuronal](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[Personnalisation supplémentaire possible](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [perceptron moyenné](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [machines à vecteurs de support](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |Idéal pour les ensembles de fonctionnalités de grande taille |
| [Machine à vecteurs de support localement profonde](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |Idéal pour les ensembles de fonctionnalités de grande taille |
| [Machine de point de Bayes](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **Classification multiclasse.** | | | | | |
| [régression logique](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [forêt de décision](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [jungle de décision ](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |Faible encombrement de mémoire |
| [réseau neuronal](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[Personnalisation supplémentaire possible](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [un contre tous](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |Consultez les propriétés de la méthode de deux classes hello sélectionnée |
| **Régression** | | | | | |
| [linéaire](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [linéaire bayésienne](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [forêt de décision](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [arbre de décision optimisé](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |Encombrement de mémoire important |
| [quantile de forêt rapide](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |Distributions plutôt que prédictions de points |
| [réseau neuronal](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[Personnalisation supplémentaire possible](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |Techniquement journal linéaire. Pour les décomptes prévisionnels |
| [ordinal](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |Pour la prédiction de rang |
| **Détection des anomalies** | | | | | |
| [machines à vecteurs de support](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |Particulièrement adapté aux ensembles de caractéristiques de grande taille |
| [Détection des anomalies reposant sur le PCA](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-moyennes](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |Un algorithme de clustering |

**Propriétés de l'algorithme :**

**●** -montre une excellente précision, les durées d’apprentissage rapide et l’utilisation de hello de linéarité

**○** : bonne précision et durée d'apprentissage modérée

## <a name="algorithm-notes"></a>Notes de l'algorithme
### <a name="linear-regression"></a>Régression linéaire
Comme mentionné précédemment, [régression linéaire](https://msdn.microsoft.com/library/azure/dn905978.aspx) correspond à un jeu de données toohello ligne (ou plan ou hyperplan). Elle est très efficace, simple et rapide, mais peut être trop simpliste pour certains problèmes.
Obtenez un [didacticiel relatif à la régression linéaire](machine-learning-linear-regression-in-azure.md)ici.

![Données avec une tendance linéaire][3]

***Données avec une tendance linéaire***

### <a name="logistic-regression"></a>Régression logique
Bien qu’il inclue confusion avec 'régression' dans le nom de hello, la régression logistique est en fait un outil puissant pour [deux classes](https://msdn.microsoft.com/library/azure/dn905994.aspx) et [multiclass](https://msdn.microsoft.com/library/azure/dn905853.aspx) classification. Elle est rapide et simple. Hello du fait qu’il utilise une '-courbe mis en forme au lieu d’une ligne droite rend naturellement pour diviser les données en groupes. La régression logique crée des limites de classes linéaires : vérifiez donc qu'une approximation linéaire vous convient.

![Données de classe tootwo de régression logistique avec simplement une fonction][4]

***Données tootwo classe la régression logistique avec simplement une fonction*** *-la limite de classe est le point hello quels hello courbe logistique est simplement plus près tooboth classes*

### <a name="trees-forests-and-jungles"></a>Arbres, forêts et jungles
Les forêts de décision ([régression](https://msdn.microsoft.com/library/azure/dn905862.aspx), [deux classes](https://msdn.microsoft.com/library/azure/dn906008.aspx) et [classes multiples](https://msdn.microsoft.com/library/azure/dn906015.aspx)), les jungles de décision ([deux classes](https://msdn.microsoft.com/library/azure/dn905976.aspx) et [classes multiples](https://msdn.microsoft.com/library/azure/dn905963.aspx)) et les arbres de décision renforcés ([régression](https://msdn.microsoft.com/library/azure/dn905801.aspx) et [deux classes](https://msdn.microsoft.com/library/azure/dn906025.aspx)) sont tous basés sur les arbres de décision, un concept fondamental pour l’apprentissage automatique. Il existe de nombreuses variantes d’arbres de décision, mais ils font tous la même chose : subdiviser l’espace de fonctionnalité hello en régions avec principalement hello même étiquette. Il peut s'agir des régions de catégorie ou de valeur constante, si vous effectuez une classification ou une régression.

![Arbre de décision subdivisant un espace de caractéristiques][5]

***Un arbre de décision divise un espace de caractéristique en régions de valeurs à peu près uniformes***

Un espace de fonctionnalités peut être subdivisé en régions arbitrairement petites, il est facile tooimagine divisant finement suffisamment toohave un point de données par région. Il s’agit d’un exemple extrême de dépassement. Dans l’ordre tooavoid cela, un grand ensemble d’arbres sont construits avec un soin particulier mathématique pris que les arborescences de hello ne sont pas corrélés. moyenne de Hello de cette forêt de décision « » est une arborescence qui permet d’éviter le surajustement. Les forêts de décision peuvent utiliser beaucoup de mémoire. Jungle d’arbres de décision est une variante qui consomme moins de mémoire à des frais de hello de légèrement plus de temps d’apprentissage.

Les arbres de décision améliorée évitent le surajustement en limitant le nombre de subdivisions et le nombre minimum de points de données autorisés dans chaque région. L’algorithme construit une séquence d’arborescences, chacune d’elles a appris pour compenser l’erreur hello d’arborescence hello avant vers la gauche. résultat de Hello est un apprenant très précis ayant tendance toouse beaucoup de mémoire. Pour hello description complète, consultez [livre de d’origine de Friedman](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[Un rapide de régression quantile de forêt](https://msdn.microsoft.com/library/azure/dn913093.aspx) est une variante d’arbres de décision pour les cas spéciaux hello dans lequel vous souhaitez connaître non seulement hello classique (médiane) valeur de données hello dans une région, mais également sa distribution sous forme de hello de quantiles.

### <a name="neural-networks-and-perceptrons"></a>Perceptrons et réseaux neuronaux
Les réseaux neuronaux sont des algorithmes d’apprentissage inspirés du cerveau couvrant les problèmes [de classes multiples](https://msdn.microsoft.com/library/azure/dn906030.aspx), [à deux classes](https://msdn.microsoft.com/library/azure/dn905947.aspx) et de [régression](https://msdn.microsoft.com/library/azure/dn905924.aspx). Ils sont disponibles dans une variété illimitée, mais hello les réseaux neuronaux dans Azure Machine Learning sont tous sous forme de hello de graphiques acycliques dirigés. Cela signifie que les fonctionnalités d'entrée sont transmises vers l'avant (jamais vers l'arrière) via une séquence de couches, avant d'être transformées en sorties. Dans chaque couche, les entrées sont pondérées dans différentes combinaisons, additionnées et transmis à la couche suivante de hello. Cette combinaison de résultats des calculs simples dans la possibilité de toolearn sophistiquées apparemment classe les données et les limites des tendances, par magie. Réseaux de plusieurs couches de ce type effectuent hello « formation approfondie » qui alimente la création de rapports bien tech et science-fiction.

Ces performances élevées ont toutefois un prix. Réseaux neuronaux peuvent prendre un tootrain beaucoup de temps, en particulier pour les grands jeux de données avec un grand nombre de fonctionnalités. Ils ont également davantage de paramètres que la plupart des algorithmes, ce qui signifie que le balayage des paramètres développe beaucoup de temps d’apprentissage hello.
Et pour ces overachievers qui souhaitent trop[spécifier leur propre structure de réseau](http://go.microsoft.com/fwlink/?LinkId=402867), les possibilités sont inexhaustible.

![Limites appris par les réseaux neuronaux][6]
***limites hello appris par les réseaux neuronaux peuvent être complexes et irrégulières***

Hello [deux classes averaged perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx) est les durées d’apprentissage des réseaux neuronaux réponse tooskyrocketing. Il utilise une structure de réseau qui fournit des limites de la classe linéaire. Il est presque primitif aux normes actuelles, mais il a un long historique de l’utilisation de manière fiable et est assez petit toolearn rapidement.

### <a name="svms"></a>Machines à vecteurs de support (SVM)
Machines à vecteurs de support (SVM) de trouver les limites hello qui sépare les classes par large une marge que possible. En cas de deux classes de hello ne peut pas être clairement séparées, les algorithmes hello trouver limite de meilleures hello que car elles peuvent. Lors de l’écriture dans Azure Machine Learning, hello [deux classes SVM](https://msdn.microsoft.com/library/azure/dn905835.aspx) avec une ligne droite uniquement. (Dans le jargon SVM, elle utilise un noyau linéaire). Car elle rend cette approximation linéaire, il est en mesure de toorun assez rapidement. Elle est particulièrement utile pour les données avec de nombreuses fonctionnalités comme les données textuelles ou de génome. Dans ces cas SVM sont tooseparate en mesure de classes plus rapidement et avec moins le surajustement que la plupart des autres algorithmes, en outre toorequiring uniquement une petite quantité de mémoire.

![Frontière de classe de machine à vecteurs de support][7]

***Une limite de classe de prise en charge de type vecteur machine optimise la marge hello séparant deux classes***

Un autre produit de Microsoft Research, hello [SVM localement approfondie de deux classes](https://msdn.microsoft.com/library/azure/dn913070.aspx) est un variant non linéaire de SVM qui conserve la majeure partie de l’efficacité de vitesse et de la mémoire hello de version linéaire de hello. Il est idéal pour les cas où les approche linéaire hello ne donnent pas de réponses suffisamment précis. les développeurs de Hello conservé rapide en divisant à problème hello dans une série de petits problèmes SVM linéaires. Hello de lecture [complète description](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) pour plus d’informations sur la façon dont ils extraite cela en hello.

À l’aide d’une extension intelligente de SVM non linéaires, hello [SVM à une classe](https://msdn.microsoft.com/library/azure/dn913103.aspx) Dessine une limite qui met en évidence étroitement hello tout jeu de données. Elle est utile pour la détection des anomalies. Les nouveaux points de données qui se trouvent bien en dehors de cette limite sont assez inhabituel toobe dignes d’intérêt.

### <a name="bayesian-methods"></a>Méthodes bayésiennes
Les méthodes bayésiennes ont une qualité très intéressante : elles évitent le surajustement. Pour cela, ils qui effectue des hypothèses au préalable distribution susceptibles de hello des réponses hello. Un autre avantage de cette approche est qu'elle a très peu de paramètres. Azure Machine Learning a des algorithmes bayésiens pour la classification ([machine de points à deux classes de Bayes](https://msdn.microsoft.com/library/azure/dn905930.aspx)) et la régression ([régression linéaire bayésienne](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Notez que ces supposent que les données de salutation peuvent être fractionner ou ajuster avec une ligne droite.

Anecdote historique, les machines de point de Bayes ont été développées par Microsoft Research. Elles reposent sur un travail théorique exceptionnel. étudiant intéressées de Hello est dirigée toohello [article d’origine dans JMLR](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) et un [blog détaillé par Chris Bishop](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx).

### <a name="specialized-algorithms"></a>Algorithmes spécialisés
Avoir un objectif très spécifique peut être bénéfique. Au sein de la collection d’Azure Machine Learning de hello, il existe des algorithmes spécialisés dans :

- Prédiction de classement ([régression ordinale](https://msdn.microsoft.com/library/azure/dn906029.aspx))
- Prédiction de nombres ([régression Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx))
- Détection des anomalies (un reposant sur [l’analyse des principaux composants](https://msdn.microsoft.com/library/azure/dn913102.aspx) et un autre sur les [machines à vecteurs de support](https://msdn.microsoft.com/library/azure/dn913103.aspx))
- Clustering ([K-moyennes](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![Détection des anomalies reposant sur le PCA][8]

***Détection d’anomalie basée sur l’ACP*** *-hello grande majorité des données de salutation se situe dans une distribution stereotypical ; points considérablement libertés avec cette distribution sont suspects*

![Jeu de données regroupé à l'aide de K-moyennes][9]

***Un jeu de données est regroupé dans cinq clusters à l’aide de K-moyennes.***

Il existe également un ensemble [one-v-all un classifieur multiclasse](https://msdn.microsoft.com/library/azure/dn905887.aspx), quel problème de classification sauts hello N-classe des problèmes de classification à deux classes n-1. analyse de précision Hello, temps d’apprentissage et les propriétés de la linéarité sont déterminées par classifieurs à deux classes hello utilisés.

![Classifieurs à deux classes combinées tooform un classifieur trois-classe][10]

***Une paire de classifieurs à deux classes combiner tooform un classifieur trois-classe***

Azure Machine Learning inclut également le framework d’apprentissage automatique puissant tooa accès sous le titre hello de [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
VW défie la catégorisation ici, puisqu'elle peut apprendre des problèmes de classification et de régression et même utiliser des données partiellement sans étiquette. Vous pouvez configurer toouse l’un des différents algorithmes, les fonctions de la perte et les algorithmes d’optimisation de la formation. Il a été conçu de hello toobe extrêmement rapide et parallèle efficace d’arrière-plan. Elle gère d’immenses ensembles de fonctionnalités avec peu d'effort.
Lancée et dirigée par John Langford de Microsoft Research, VW est une Formule 1 dans la course des algorithmes. VW le mieux à tous les problèmes, mais si le vôtre n’est le cas, il peut être avantageux tooclimb la courbe d’apprentissage sur son interface. Elle est également disponible en tant que [code open source autonome](https://github.com/JohnLangford/vowpal_wabbit) dans plusieurs langues.

## <a name="more-help-with-algorithms"></a>Aide supplémentaire sur les algorithmes
* Pour obtenir une infographie téléchargeable décrivant les algorithmes et fournissant des exemples, consultez [Infographie téléchargeable : Principes de base de l’apprentissage automatique avec exemples d’algorithmes](machine-learning-basics-infographic-with-algorithm-examples.md).
* Pour obtenir une liste par catégorie des algorithmes d’apprentissage automatique hello tous les disponibles dans Azure Machine Learning Studio, consultez [initialiser le modèle] [ initialize-model] hello Machine Learning Studio algorithme et aide du Module.
* Pour obtenir la liste alphabétique complète des algorithmes et des modules de Azure Machine Learning Studio, consultez [Liste alphabétique des modules de Machine Learning Studio][a-z-list] dans Machine Learning Studio : aide sur les algorithmes et les modules.
* toodownload et imprimer un diagramme qui donne une vue d’ensemble des fonctionnalités de hello d’Azure Machine Learning Studio, consultez [diagramme de vue d’ensemble des fonctionnalités d’Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
