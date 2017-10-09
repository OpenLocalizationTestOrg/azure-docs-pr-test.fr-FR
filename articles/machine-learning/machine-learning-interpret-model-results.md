---
title: "résultats du modèle aaaInterpret dans l’apprentissage | Documents Microsoft"
description: "Comment paramètre optimal de hello toochoose définie un algorithme à l’aide et de visualisation des sorties de modèle de score."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Interprétation des résultats de modèle dans Azure Machine Learning
Cette rubrique explique comment toovisualize et interpréter les résultats de prédiction dans Azure Machine Learning Studio. Après avoir formé d’un modèle et effectue des prédictions par-dessus (« modèle de hello transformée »), vous devez toounderstand et interpréter les résultats de prédiction hello.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Il existe quatre principaux types de modèles d'apprentissage automatique dans Azure Machine Learning :

* classification ;
* clustering.
* régression ;
* systèmes de recommandation.

les modules de Hello utilisés pour la prédiction sur ces modèles sont :

* [Noter le modèle][score-model] pour la classification et la régression
* [Affecter tooClusters] [ assign-to-clusters] module pour le clustering
* [Noter la recommandation Matchbox][score-matchbox-recommender] pour les systèmes de recommandation

Ce document explique l’affichage des résultats de prédiction de toointerpret pour chacun de ces modules. Pour une vue d’ensemble de ces modules, consultez [comment toochoose paramètres toooptimize vos algorithmes dans Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).

Cette rubrique aborde l’interprétation des prédictions et non l’évaluation du modèle. Pour plus d’informations sur la façon tooevaluate votre modèle, consultez [comment tooevaluate modèle de performances dans Azure Machine Learning](machine-learning-evaluate-model-performance.md).

Si vous êtes tooAzure nouvelle Machine Learning et que vous avez besoin d’aide à la création d’un tooget une expérience simple démarré, consultez [créer une expérience simple dans Azure Machine Learning Studio](machine-learning-create-experiment.md) dans Azure Machine Learning Studio.

## <a name="classification"></a>Classification
Il existe deux sous-catégories de problèmes de classification :

* Problèmes avec uniquement deux classes (classification double classe ou binaire)
* Problèmes avec plus de deux classes (classification multiclasse)

Azure Machine Learning a toodeal différents modules avec chacun de ces types de classification, mais les méthodes hello pour interpréter leurs résultats de prédiction sont similaires.

### <a name="two-class-classification"></a>Classification double classe.
**Exemple d'expérience**

Un exemple d’un problème de classification à deux classes est classification hello de fleurs d’iris. tâche Hello est fleurs d’iris tooclassify en fonction de leurs fonctionnalités. jeu de données Iris fourni dans Azure Machine Learning Hello est un sous-ensemble de hello populaires [jeu de données Iris](http://en.wikipedia.org/wiki/Iris_flower_data_set) contenant des instances de seulement deux fleur espèces (classes 0 et 1). Chaque fleur comporte quatre caractéristiques (la longueur des sépales, la largeur des sépales, la longueur des pétales et la largeur des pétales).

![Capture d’écran de l’expérience iris](./media/machine-learning-interpret-model-results/1.png)

Figure 1. Expérience d’un problème de classification double classe iris

Une expérience été effectuée toosolve ce problème, comme illustré dans la Figure 1. Un modèle d'arbre de décision augmentée, double classe a été formé et noté. Maintenant vous permet de visualiser les résultats de prédiction hello de hello [Score Model] [ score-model] module en cliquant sur le port de sortie hello Hello [Score Model] [ score-model]module et en cliquant sur **visualiser**.

![Module Noter le modèle](./media/machine-learning-interpret-model-results/1_1.png)

Hello score des résultats comme indiqué dans la Figure 2 s’affiche.

![Résultats de l’expérience de classification double classe iris](./media/machine-learning-interpret-model-results/2.png)

Figure 2 : Visualisation du résultat du modèle de notation dans la classification double classe

**Interprétation du résultat**

Il y a six colonnes dans la table des résultats hello. colonnes de quatre gauche Hello sont des fonctionnalités de quatre hello. Hello droite deux colonnes, Scored Labels et probabilités évaluées, sont des résultats de prédiction hello. Hello notées les probabilités colonne montre hello probabilité qu’un fleuriste appartienne toohello de classe positif (classe 1). Par exemple, hello premier numéro de moyens de colonne (0.028571) hello est 0.028571 probabilité hello fleur première appartient tooClass 1. Hello Scored Labels colonne montre hello prévisible de classe pour chaque fleur. Cela est basée sur la colonne des probabilités de transformée hello. Si hello transformée la probabilité d’un fleuriste est supérieure à 0,5, il est prévu en tant que classe 1. Sinon, elle est prédite en tant que classe 0.

**Publication du service web**

Une fois les résultats de prédiction hello ont été compris et jugées audio, hello expérience peut être publié en tant qu’un service web afin que vous pouvez déployer dans différentes applications et appeler des prédictions de classe tooobtain sur n’importe quel fleur iris nouvelle. toolearn toochange une formation faire des essais en expérience de score et le publier en tant qu’un service web, voir [publier le service web de Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md). Cette procédure vous permet de bénéficier d’une expérience de notation, comme indiqué dans la Figure 3.

![Capture d’écran de l’expérience de notation](./media/machine-learning-interpret-model-results/3.png)

Figure 3. Calcul de score expérience de problème de classification à deux classes hello iris

Vous devez maintenant tooset hello entrée et sortie pour le service web de hello. entrée Hello est port d’entrée de droite hello de [Score Model][score-model], qui est hello Iris fleur fonctionnalités entrée. Hello choix de la sortie de hello varie selon que vous sont intéressées Bonjour prédit classe (étiquette noté), hello transformée probabilité ou les deux. Dans cet exemple, on considère ici que vous êtes intéressé par les deux. tooselect hello souhaitée des colonnes de sortie, utilisez un [sélectionner les colonnes dans le jeu de données] [ select-columns] module. Cliquez sur le module [Sélectionner des colonnes dans le jeu de données][select-columns], sur **Lancer le sélecteur de colonne** situé dans le volet droit, puis sélectionnez **Étiquettes notées** et **Probabilités notées**. Après avoir défini le port de sortie hello du [sélectionner les colonnes dans le jeu de données] [ select-columns] et exécuter à nouveau, vous devez être prêt toopublish expérience de score hello comme un service web en cliquant sur **publier le site WEB SERVICE**. expérience de final Hello ressemble à la Figure 4.

![expérience de classification à deux classes Hello iris](./media/machine-learning-interpret-model-results/4.png)

Figure 4. Expérience de notation finale d’un problème de classification double classe Iris

Après avoir exécuté le service web de hello et que vous entrez des valeurs de certaines fonctionnalités d’une instance de test, le résultat de hello renvoie deux nombres. numéro de la première Hello est hello transformée étiquette et hello est ensuite hello transformée probabilité. Cette fleur est prédite en tant que Classe 1 avec une probabilité de 0,9655.

![Test de l’interprétation Noter le modèle](./media/machine-learning-interpret-model-results/4_1.png)

![Résultats du test d’évaluation](./media/machine-learning-interpret-model-results/5.png)

Figure 5. Résultat du service web de classification double classe Iris

### <a name="multi-class-classification"></a>Classification multiclasse.
**Exemple d'expérience**

Lors de cette expérience, vous réalisez une tâche de reconnaissance de lettres en tant qu’exemple de classification multiclasse. Hello classifieur tente toopredict une certaine lettre (classe) en fonction de certaines valeurs d’attribut de manuel extraites à partir d’images de hello écrit manuellement.

![Exemple de reconnaissance de lettres](./media/machine-learning-interpret-model-results/5_1.png)

Dans les données d’apprentissage hello, il existe des 16 fonctionnalités extraites à partir d’images de lettre de manuel. Hello 26 lettres forment nos 26 classes. La figure 6 montre une expérience qui sera l’apprentissage d’une classification multiclasse de modèle pour la reconnaissance des lettres et prédire sur hello même fonctionnalité ensemble sur un jeu de données de test.

![Expérience de classification multiclasse de reconnaissance de lettre](./media/machine-learning-interpret-model-results/6.png)

Figure 6. Expérience de problème de classification multiclasse de reconnaissance de lettre

Visualisation des résultats hello de hello [Score Model] [ score-model] module en cliquant sur le port de sortie hello du [Score Model] [ score-model] module, puis en cliquant sur **visualiser**, vous devez voir le contenu comme indiqué dans la Figure 7.

![Résultats Noter le modèle](./media/machine-learning-interpret-model-results/7.png)

Figure 7. Visualisation du résultat de modèle de notation dans la classification multiclasse

**Interprétation du résultat**

colonnes de 16 gauche Hello représentent les valeurs de fonctionnalité hello de jeu de test hello. colonnes Hello avec des noms, telles que les probabilités d’évaluées pour la classe « XX » sont comme colonne des probabilités de transformée hello dans les cas de deux classes hello. Ils montrent la probabilité hello hello entrée correspondante se situe dans une certaine classe. Par exemple, pour la première entrée de hello, il est 0.003571 probabilité qu’il s’agit d’un « A », 0.000451 probabilité qu’il s’agit d’un « B » et ainsi de suite. colonne de dernière Hello (étiquettes au score calculé) est hello identique dans les cas de deux classes hello Scored Labels. Il sélectionne la classe hello avec hello plus grande transformée probabilité comme hello classe prévue de l’entrée correspondante de hello. Par exemple, pour la première entrée de hello, hello transformée étiquette est « F », car il a hello plus grande probabilité toobe (0.916995) « F ».

**Publication du service web**

Vous pouvez également obtenir hello évalué d’étiquette pour chaque entrée et hello probabilité hello transformée d’étiquette. logique de base Hello représente la probabilité de plus grande de hello toofind entre hello toutes les probabilités de transformée. toodo, vous devez toouse hello [Execute R Script] [ execute-r-script] module. Hello code R est indiqué dans la Figure 8, et résultat hello d’expérimentation de hello est indiqué dans la Figure 9.

![Exemple de code R](./media/machine-learning-interpret-model-results/8.png)

Figure 8. Code R d’extraction Scored Labels et hello associées des probabilités des étiquettes de hello

![Résultat de l’expérience](./media/machine-learning-interpret-model-results/9.png)

Figure 9. Expérience de score final de problème de classification multiclasse de reconnaissance de lettre hello

Une fois que vous publiez et exécutez le service web de hello et entrez des valeurs de la fonctionnalité d’entrée, hello renvoyé de résultat ressemble à la Figure 10. Cette lettre manuel, avec ses fonctionnalités de 16 extraites est prédite toobe un « T » avec une probabilité 0.9715.

![Test de l’interprétation du module de notation](./media/machine-learning-interpret-model-results/9_1.png)

![Résultat de test](./media/machine-learning-interpret-model-results/10.png)

Figure 10. Résultat du service web de classification multiclasse

## <a name="regression"></a>régression ;
Les problèmes de régression sont différents des problèmes de classification. Un problème de classification, que vous essayez toopredict classes discrètes, telles que la classe appartient un fleuriste iris. Mais comme vous pouvez le voir dans hello exemple d’un problème de régression suivant, que vous essayez de toopredict une variable continue, comme les prix hello d’une voiture.

**Exemple d'expérience**

Utilisez la prédiction du prix d’une voiture comme exemple de régression. Vous essayez de prix de hello toopredict d’une voiture en fonction de ses fonctionnalités, y compris la marque, type de carburant, type de corps et la roulette de lecteur. expérience de Hello est illustrée dans la Figure 11.

![Expérience de régression de prix des véhicules automobiles](./media/machine-learning-interpret-model-results/11.png)

Figure 11. Expérience de problème de régression de prix des véhicules automobiles

Visualisation hello [Score Model] [ score-model] module, résultat de hello ressemble à la Figure 12.

![Résultats d’évaluation pour le problème de prédiction du prix des véhicules automobiles](./media/machine-learning-interpret-model-results/12.png)

Figure 12 : Résultat du calcul de score pour problème de prédiction de prix automobile hello

**Interprétation du résultat**

Étiquettes évaluées est la colonne de résultat hello dans ce résultat du calcul de score. les numéros de Hello sont des prix prédite de hello pour chaque voiture.

**Publication du service web**

Vous pouvez publier l’expérience de régression hello dans un service web et l’appeler pour la prédiction de prix automobile Bonjour la même façon que dans classification à deux classes hello les cas d’usage.

![Expérience de notation pour le problème de prédiction du prix des véhicules automobiles](./media/machine-learning-interpret-model-results/13.png)

Figure 13 : Expérience de notation pour un problème de prédiction du prix des véhicules automobiles

En cours d’exécution service web de hello, hello retourné résultat ressemble à la Figure 14. prix de prédite Hello pour cette voiture est $15,085.52.

![Module de notation d’interprétation de test](./media/machine-learning-interpret-model-results/13_1.png)

![Résultats du module de notation](./media/machine-learning-interpret-model-results/14.png)

Figure 14. Résultat du service web d’un problème de régression du prix d’une voiture

## <a name="clustering"></a>clustering.
**Exemple d'expérience**

Nous allons utiliser hello jeu de données Iris à nouveau toobuild une expérience de gestion de clusters. Ici, vous pouvez filtrer les étiquettes de classe hello dans le jeu de données hello afin qu’il dispose de fonctionnalités et peut être utilisé pour le clustering d’uniquement. Cas d’usage dans cette iris, spécifiez les nombre hello de clusters toobe, deux au cours du processus d’apprentissage hello, ce qui signifie que vous serez cluster fleurs de hello en deux classes. expérience de Hello est indiqué dans la Figure 15.

![Expérience d’un problème de clustering Iris](./media/machine-learning-interpret-model-results/15.png)

Figure 15. Expérience d’un problème de clustering Iris

Clustering est différente de classification dans le jeu de données d’apprentissage hello n’a pas les étiquettes réalité de terrain par lui-même. Groupes de clusters hello instances du jeu de données d’apprentissage en clusters distincts. Au cours du processus d’apprentissage hello, les étiquettes de modèle hello hello entrées par apprentissage des différences de hello entre leurs fonctionnalités. Après cela, d’utiliser le modèle formé hello toofurther classer les entrées ultérieures. Il existe deux parties de résultat hello que nous intéresse au sein d’un problème de gestion de clusters. première partie de Hello est étiquetage de jeu de données d’apprentissage hello et hello est ensuite classer un nouveau jeu de données avec le modèle formé de hello.

Hello première partie du résultat de hello peut être visualisé en cliquant sur hello gauche du port de sortie du [Train Clustering Model] [ train-clustering-model] , puis en cliquant sur **visualiser**. visualisation de Hello est indiquée dans la Figure 16.

![Résultat du clustering](./media/machine-learning-interpret-model-results/16.png)

Figure 16. Visualiser le résultat pour le jeu de données d’apprentissage hello de clustering

résultat de Hello de deuxième partie hello, clustering des nouvelles entrées avec le modèle de clustering formé hello, est illustré dans la Figure 17.

![Visualiser le résultat de clustering](./media/machine-learning-interpret-model-results/17.png)

Figure 17. Visualisation du résultat de clustering sur un nouveau jeu de données

**Interprétation du résultat**

Bien que les résultats hello de parties de hello deux proviennent d’expériences dans différentes phases, elles apparaîtront hello identiques et sont interprétées dans hello identique. Hello quatre premières colonnes sont des fonctionnalités. dernière colonne Hello, affectations, est le résultat de prédiction hello. Bonjour Bonjour d’affectées même nombre prévues toobe Bonjour même cluster, autrement dit, ils partagent les similitudes d’une certaine façon (cette expérience utilise les mesures de distance EUCLIDIENNE hello par défaut). Étant donné que vous avez spécifié le nombre de hello de clusters toobe 2, entrées hello dans les attributions sont étiquetées 0 ou 1.

**Publication du service web**

Vous pouvez publier hello clustering expérience dans un service web et l’appeler pour le clustering des prédictions hello même façon que les cas d’usage dans la classification à deux classes hello.

![Expérience de notation d’un problème de clustering Iris](./media/machine-learning-interpret-model-results/18.png)

Figure 18. Expérience de notation d’un problème de clustering Iris

Après avoir exécuté le service web de hello, hello retourné le résultat ressemble à la Figure 19. Cette fleur est prédite toobe cluster 0.

![Module de notation d’interprétation de test](./media/machine-learning-interpret-model-results/18_1.png)

![Résultat du module de notation](./media/machine-learning-interpret-model-results/19.png)

Figure 19. Résultat du service web de classification double classe Iris

## <a name="recommender-system"></a>Système de recommandation
**Exemple d'expérience**

Pour les systèmes de recommandation, vous pouvez utiliser le problème de recommandation hello restaurant par exemple : vous pouvez recommander des restaurants pour les clients en fonction de leur historique d’évaluation. les données d’entrée Hello se compose de trois parties :

* Notations de restaurants attribuées par les clients
* Données caractéristiques des clients
* Données sur les caractéristiques de restaurants

Il existe plusieurs choses que nous pouvons faire avec hello [Train Matchbox Recommender] [ train-matchbox-recommender] module dans Azure Machine Learning :

* Prédire des notations pour un utilisateur et un élément donné
* Recommandons tooa éléments donné utilisateur
* Rechercher des utilisateurs tooa connexes donné utilisateur
* Rechercher des éléments connexes tooa est donné d’élément

Vous pouvez choisir ce que vous souhaitez toodo en sélectionnant options hello quatre Bonjour **type de prédiction Recommender** menu. Vous pouvez parcourir quatre scénarios.

![Recommandation matchbox](./media/machine-learning-interpret-model-results/19_1.png)

Une expérience Azure Machine Learning type pour un système de recommandation est semblable à celui de la Figure 20. Pour plus d’informations sur comment toouse ces modules système de recommandation, consultez [de recommandations matchbox Train] [ train-matchbox-recommender] et [Score de recommandations matchbox] [ score-matchbox-recommender].

![Expérience du système de recommandation](./media/machine-learning-interpret-model-results/20.png)

Figure 20. Expérience du système de recommandation

**Interprétation du résultat**

**Prédire des notations pour un utilisateur et un élément donné**

En sélectionnant **une prédiction d’évaluation** sous **type de prédiction Recommender**, vous demandez recommender de hello hello toopredict de système d’évaluation pour un utilisateur donné et un élément. Hello visualisation Hello [Score Matchbox Recommender] [ score-matchbox-recommender] sortie ressemble à la Figure 21.

![Résultat de système de recommandation hello : prédiction de l’évaluation de score](./media/machine-learning-interpret-model-results/21.png)

Figure 21. Visualiser les résultats de score hello de système de recommandation hello : prédiction d’évaluation

Hello deux premières colonnes sont des paires utilisateur-élément de hello fournis par les données d’entrée hello. troisième colonne de Hello est hello évaluation prédite d’un utilisateur pour un article donné. Par exemple, dans la première ligne de hello, client U1048 prédit toorate restaurant 135026 2.

**Recommandons tooa éléments donné utilisateur**

En sélectionnant **recommandation d’élément** sous **type de prédiction Recommender**, vous vous demandez recommender de hello système toorecommend éléments tooa donné utilisateur. Hello dernier paramètre toochoose dans ce scénario est *recommandé de sélection d’éléments*. Hello option **d’éléments d’évalués (pour l’évaluation de modèle)** est principalement utilisé pour l’évaluation du modèle pendant le processus d’apprentissage hello. Pour cette étape de prédiction, nous choisissons **À partir de tous les éléments**. Hello visualisation Hello [Score Matchbox Recommender] [ score-matchbox-recommender] sortie ressemble à la Figure 22.

![Visualisation du résultat de notation du système de recommandation - Recommandation d’éléments](./media/machine-learning-interpret-model-results/22.png)

Figure 22. Visualiser le résultat de score de système de recommandation hello--recommandation d’élément

Bonjour premier Hello de représente hello six colonnes donné d’éléments de toorecommend l’ID utilisateur, tel que fourni par les données d’entrée hello. Hello cinq autres colonnes représentent les éléments hello recommandés utilisateur toohello par ordre décroissant de pertinence. Par exemple, dans la première ligne de hello, hello plus recommandé restaurant client U1048 est 134986, suivie de 135018, 134975, 135021 et 132862.

**Rechercher des utilisateurs tooa connexes donné utilisateur**

En sélectionnant **utilisateurs liés** sous **type de prédiction Recommender**, vous vous demandez recommender de hello utilisateur système toofind d’utilisateurs liés tooa donné. Les utilisateurs associés sont des utilisateurs de hello qui ont des préférences similaires. Hello dernier paramètre toochoose dans ce scénario est *liés de sélection de l’utilisateur*. Hello option **d’utilisateurs ayant évalué des éléments (pour l’évaluation de modèle)** est principalement utilisé pour l’évaluation du modèle pendant le processus d’apprentissage hello. Pour cette étape de prédiction, choisissez **À partir de tous les utilisateurs**. Hello visualisation Hello [Score Matchbox Recommender] [ score-matchbox-recommender] sortie ressemble à la Figure 23.

![Visualisation du résultat de notation du système de recommandation - Utilisateurs associés](./media/machine-learning-interpret-model-results/23.png)

Figure 23. Visualiser les résultats du score de système de recommandation hello--utilisateurs liés

Hello tout d’abord de hello de montre hello six colonnes donnée utilisateur ID nécessités toofind liées aux utilisateurs, tel que fourni par les données d’entrée. Hello autre banque de cinq colonnes hello utilisateurs liés prédits d’utilisateur hello dans l’ordre décroissant de pertinence. Par exemple, dans la première ligne de hello, client les plus pertinents hello client U1048 est U1051, suivie de U1066, U1044, U1017 et U1072.

**Rechercher des éléments connexes tooa est donné d’élément**

En sélectionnant **éléments connexes** sous **type de prédiction Recommender**, vous demandez recommender de hello élément tooa donné du système toofind éléments connexes. Liés à des éléments sont toobe probablement des éléments de hello aimé par hello même utilisateur. Hello dernier paramètre toochoose dans ce scénario est *liés de sélection d’éléments*. Hello option **d’éléments d’évalués (pour l’évaluation de modèle)** est principalement utilisé pour l’évaluation du modèle pendant le processus d’apprentissage hello. Pour cette étape de prédiction, nous choisissons **À partir de tous les éléments** . Hello visualisation Hello [Score Matchbox Recommender] [ score-matchbox-recommender] sortie ressemble à la Figure 24.

![Visualisation du résultat de notation du système de recommandation - articles associés](./media/machine-learning-interpret-model-results/24.png)

Figure 24. Visualiser les résultats du score de système de recommandation hello--éléments connexes

Hello premier Hello de représente hello six colonnes étant donné les ID d’éléments nécessités toofind les éléments liés aux, tel que fourni par les données d’entrée hello. Hello autre banque de cinq colonnes hello éléments liés prédits d’élément hello dans l’ordre décroissant en termes de pertinence. Par exemple, dans la première ligne de hello, élément de hello les plus pertinents pour l’élément 135026 est 135074, suivie de 135035, 132875, 135055 et 134992.

**Publication du service web**

processus de Hello de ces expériences en tant que prédictions de tooget de services web de publication est similaire pour chacun des quatre scénarios de hello. Ici, nous prenons second scénario de hello (il est recommandé d’éléments tooa donné utilisateur) comme exemple. Vous pouvez suivre hello même procédure avec hello trois autres.

Enregistrement hello formé de système de recommandation comme un modèle formé et le filtrage tooa des données d’entrée hello colonne d’ID utilisateur unique comme demandé, vous pouvez raccorder expérience hello comme dans la Figure 25 et publier en tant que service web.

![Expérience de problème de recommandation hello restaurant de calcul de score](./media/machine-learning-interpret-model-results/25.png)

Figure 25. Expérience de problème de recommandation hello restaurant de calcul de score

En cours d’exécution service web de hello, hello retourné de résultats ressemble Figure 26. les restaurants recommandée cinq Hello pour utilisateur U1048 sont 134986, 135018, 134975, 135021 et 132862.

![Exemple de service de système de recommandation](./media/machine-learning-interpret-model-results/25_1.png)

![Résultat de l’exemple d’expérience](./media/machine-learning-interpret-model-results/26.png)

Figure 26. Résultat du service web d’un problème de recommandation de restaurants

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
