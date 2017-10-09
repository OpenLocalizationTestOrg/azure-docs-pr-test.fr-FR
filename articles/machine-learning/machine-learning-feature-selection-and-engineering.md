---
title: "aaaFeature l’ingénierie et la sélection dans Azure Machine Learning | Documents Microsoft"
description: "Explique à des fins de hello de sélection de fonctionnalités et l’ingénierie de fonctionnalité et fournit des exemples de leur rôle dans le processus d’amélioration des données hello de l’apprentissage."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Ingénierie et sélection de caractéristiques dans Azure Machine Learning
Cette rubrique explique à des fins de hello d’ingénierie de fonctionnalité et de sélection des fonctionnalités dans le processus d’amélioration des données hello de l’apprentissage. Elle présente les étapes de ces processus à l’aide des exemples fournis par Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

données d’apprentissage Hello en apprentissage peuvent souvent être améliorées par la sélection de hello ou l’extraction de fonctionnalités à partir des données brutes de hello collectées. Un exemple d’une fonction d’ingénierie dans le contexte hello d’apprendre comment tooclassify hello de caractères manuscrites est un mappage de densité de bits construits à partir de données de distribution bits bruts hello. Ce mappage permet de rechercher des bords hello de caractères de hello plus efficacement que la distribution de brut hello.

Fonctionnalités d’ingénierie et sélectionnées accroître l’efficacité de hello du processus d’apprentissage hello, qui essaie d’informations de clé de hello tooextract contenues dans les données de salutation. Ils améliorent également power hello de ces modèles tooclassify hello d’entrée de données avec précision et toopredict des résultats d’intéressent plus efficacement. Ingénierie de fonctionnalité et de sélection peuvent également combiner des toomake d’apprentissage automatique hello en plus de calculs souple. Il le fait en améliorant et réduction de plusieurs fonctionnalités hello nécessaires toocalibrate ou effectuer l’apprentissage d’un modèle. Strictement mathématique, modèle de hello hello fonctionnalités tootrain sélectionné sont un ensemble minimal de variables indépendantes qui expliquent les schémas hello dans les données de salutation et puis prédire les résultats avec succès.

l’équipe d’ingénierie Hello et sélection de fonctionnalités est une partie d’un processus plus vaste, qui se compose généralement de quatre étapes :

* Collecte des données
* Amélioration des données
* Construction de modèles
* Post-traitement

L’équipe d’ingénierie et sélection composent étape d’amélioration de données hello de l’apprentissage. Trois aspects de ce processus peuvent être distingués relativement à nos objectifs :

* **Avant le traitement des données**: ce processus tooensure tentatives qui hello les données collectées est cohérent. Ce processus inclut des tâches telles que l’intégration de jeux de données multiples, la gestion des données manquantes, la gestion des données inconsistantes et la conversion des types de données.
* **L’équipe d’ingénierie de fonctionnalité**: ce processus tente de toocreate des fonctionnalités pertinentes supplémentaires dans les fonctionnalités existantes brutes hello dans hello données et tooincrease prédictif toohello algorithme d’apprentissage.
* **Sélection des fonctionnalités**: ce processus sélectionne le sous-ensemble de clé hello de données fonctionnalités tooreduce hello dimensionnalité des problème de formation hello.

Cette rubrique couvre uniquement hello fonctionnalité ingénierie et la fonctionnalité de sélection aspects hello amélioration du processus de données. Pour plus d’informations sur l’étape de prétraitement des données hello, consultez [prétraitement des données dans Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Création de caractéristiques à partir de vos données : ingénierie de caractéristiques
données d’apprentissage Hello se comprennent d’une matrice composée d’exemples (enregistrements ou observations stockées dans les lignes), chacun d’eux a un ensemble de fonctionnalités (variables ou stockées dans des colonnes de champs). fonctionnalités de Hello spécifiées dans expérimental hello sont des modèles de hello toocharacterize attendu dans les données de salutation. Bien que la plupart des champs peuvent être inclus directement dans des données brutes hello hello fonctionnalité sélectionnée jeu utilisé tootrain un modèle, des fonctionnalités supplémentaires ingénieries doivent souvent toobe construite à partir de fonctionnalités hello dans hello données brutes toogenerate un jeu de données d’apprentissage améliorée.

Quel type de fonctionnalités doit être créé de jeu de données tooenhance hello lors de l’apprentissage d’un modèle ? Ingénierie fonctionnalités qui améliorent la formation de hello fournissent des informations qui différencie mieux les modèles hello dans les données de salutation. Vous attendez hello nouvelles fonctionnalités tooprovide des informations supplémentaires qui n’est pas clairement capturé ou facile à détecter dans hello d’origine ou ensemble de fonctionnalités existantes, mais ce processus est un art. Des décisions réfléchies et productives nécessitent souvent une spécialisation dans le domaine.

Lorsque vous démarrez avec Azure Machine Learning, il est plus simple toograsp ce processus concrètement en utilisant les exemples fourni dans Machine Learning Studio. Deux exemples sont présentés ici :

* Un exemple de régression ([prédiction du nombre de hello de locations de vélo](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) dans une expérience contrôlée, où les valeurs cibles de hello sont connus
* un exemple de classification d'exploration de texte utilisant le [hachage de caractéristiques][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Exemple 1 : ajout de caractéristiques temporelles pour un modèle de régression
toodemonstrate tooengineer fonctionnalités pour une tâche de régression, nous allons suivre hello expérience « prévision de la demande de bicyclettes » dans Azure Machine Learning Studio. Hello cette expérience vise à la demande de hello toopredict des vélos hello, autrement dit, le numéro de hello de Locations bike au sein d’un mois spécifique, le jour ou une heure. jeu de données Hello **jeu de données Bike location UCI** est utilisé en tant que données d’entrée brutes de hello.

Ce jeu de données est basé sur les données réelles provenant d’hello entreprise majuscule Bikeshare qui tient à jour un réseau de location de vélo dans Washington DC Bonjour États-Unis. jeu de données Hello représente le nombre hello de locations de vélo au sein d’une heure spécifique d’une journée, à partir de 2011 too2012, et il contient 17379 lignes et 17 colonnes. ensemble de fonctionnalités brutes de Hello contient des conditions météo (température, humidité, vitesse du vent) et type hello du jour hello (jour férié ou un jour de la semaine). Hello champ toopredict est **cnt**, un nombre qui représente les locations de vélo hello au sein d’une heure spécifique et qui varie de 1 too977.

tooconstruct fonctionnalités efficaces dans les données d’apprentissage hello, quatre modèles de régression sont générés à l’aide de hello même algorithme, mais avec des données d’apprentissage différentes quatre définit. Hello quatre jeux de données représentent hello les mêmes données d’entrée brutes, mais avec un nombre croissant de fonctionnalités défini. Ces caractéristiques sont regroupées en quatre catégories :

1. A = météo, congé + weekday + week-end fonctionnalités jour prédite de hello
2. B = nombre de bicyclettes qui ont été louées dans chacun des hello 12 dernières heures
3. C = nombre de bicyclettes qui ont été louées dans chacun des hello précédentes 12 jours à hello même heure
4. D = nombre de bicyclettes qui ont été louées dans chacun des hello 12 semaines précédentes hello même heure et hello même jour

Outre la fonctionnalité set A, qui existe déjà dans les données brutes d’origine hello, hello autres trois ensembles de fonctionnalités sont créés via la fonctionnalité hello processus d’ingénierie. Ensemble de fonctionnalités B captures hello récente à la demande pour les vélos hello. Fonctionnalité définie C captures à la demande de hello pour vélos à une heure spécifique. Fonctionnalité définie à la demande de capture D pour bicyclettes à l’heure et jour de semaine de hello particulier. Chacun des jeux de données d’apprentissage hello quatre inclut des ensembles de fonctionnalités A, A + B, A + B + C et A + B + C + D, respectivement.

Bonjour expérience Azure Machine Learning, ces quatre jeux de données d’apprentissage sont formées par quatre branches à partir du jeu de données d’entrée prétraitées hello. À l’exception de branche à l’extrême gauche de hello, chacune de ces branches contient un [Execute R Script] [ execute-r-script] module dans lequel un ensemble de dérivées des fonctionnalités (fonctionnalité définit B, C et D) est respectivement construit et ajouté toohello importés de jeu de données. Hello figure suivante illustre les script hello R ensemble de fonctionnalités toocreate B dans la deuxième branche de gauche hello.

![Créer un ensemble de caractéristiques](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Hello tableau suivant récapitule comparaison hello des résultats de performance hello des quatre modèles de hello. obtenir les meilleurs résultats Hello sont affichés par les fonctionnalités A + B + C. Notez que ce taux d’erreur hello diminue lorsque les ensembles de fonctionnalités supplémentaires sont inclus dans les données d’apprentissage hello. Cette opération vérifie notre présumer que hello des ensembles de fonctionnalités B et C fournissent des informations supplémentaires pertinentes pour la tâche de régression hello. Ajout d’ensemble de fonctionnalités hello D ne semble pas tooprovide toute réduction supplémentaire de taux d’erreur hello.

![Comparer les résultats des performances](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> Exemple 2 : création de caractéristiques dans l’exploration de texte
Ingénierie de fonctionnalité est largement appliquée dans tootext associées à des tâches d’exploration de données, tels que l’analyse de classification et l’opinion de document. Par exemple, lorsque vous souhaitez que les documents tooclassify en plusieurs catégories, une hypothèse classique est que les mots de hello ou des expressions incluses dans la catégorie d’un document sont moins susceptibles de toooccur dans une autre catégorie de document. En d’autres termes, fréquence hello de distribution de mot ou une expression hello est catégories de document différent en mesure de toocharacterize. Dans les applications d’exploration de données texte, processus d’ingénierie de fonctionnalité de hello est toocreate nécessaires hello fonctionnalités de fréquences mot ou une expression, car les éléments individuels du contenu de texte généralement servent hello des données d’entrée.

tooachieve cette tâche, une technique appelée *fonctionnalité hachage* est appliqué tooefficiently activer les fonctionnalités de texte arbitraire dans l’index. Au lieu d’associer chaque fonctionnalité (mots ou expressions) tooa particulier index de texte, cette méthode fonctionne en appliquant un hachage fonction toohello de fonctionnalités et à l’aide de leurs valeurs de hachage en tant qu’index directement.

Dans Azure Machine Learning, il existe un module de [hachage de caractéristiques][feature-hashing] qui crée ces caractéristiques de mot ou expression. Hello figure suivante montre un exemple d’utilisation de ce module. jeu de données d’entrée Hello contient deux colonnes : évaluation de livre hello allant de 1 too5 hello réelle révision et contenue. objectif Hello de cette [Feature Hashing] [ feature-hashing] module est tooretrieve nouvelles fonctionnalités qui indiquent la fréquence d’occurrence hello de mots correspondants de hello ou des phrases dans la révision du livre spécifique hello. toouse ce module, vous devez hello toocomplete comme suit :

1. Colonne hello SELECT qui contient le texte d’entrée hello (**Col2** dans cet exemple).
2. Définissez *taille de bit hachage* too8, ce qui signifie que 2 ^ 8 = 256 fonctionnalités sont créées. Hello mot ou une phrase dans le texte hello est ensuite hachée too256 indices. Hello paramètre *taille de bit hachage* est comprise entre 1 too31. Si le paramètre hello a la valeur tooa plus grand nombre, hello de mots ou expressions sont moins susceptibles de toobe haché dans hello même index.
3. Définir le paramètre hello *N-grammes* too2. Il récupère la fréquence d’occurrence hello d’unigrammes (il s’agit d’une fonctionnalité pour tous les mots) et les bigrammes (il s’agit d’une fonctionnalité pour chaque paire de mots adjacents) hello texte d’entrée. Hello paramètre *N-grammes* est comprise entre 0 too10, ce qui indique le nombre maximal de hello de toobe séquentielles mots inclus dans une fonctionnalité.  

![Module hachage de caractéristiques](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Hello figure suivante illustre l’aspect de ces nouvelles fonctionnalités.

![Exemple de hachage de caractéristiques](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Filtrage des caractéristiques à partir de vos données : sélection de caractéristiques
*Sélection des fonctionnalités* est un processus qui est généralement appliqué construction toohello de jeux de données de formation pour la modélisation prédictive des tâches telles que les tâches de classification ou de régression. Hello vise tooselect un sous-ensemble de fonctionnalités hello hello d’origine jeu de données qui réduit ses dimensions à l’aide d’un ensemble minimal de fonctionnalités toorepresent hello maximum de variance dans les données de salutation. Ce sous-ensemble de fonctionnalités contient tootrain hello modèle hello uniquement fonctionnalités toobe inclus. La sélection de caractéristiques a deux principaux objectifs :

* Elle augmente souvent la précision de classification en éliminant les caractéristiques non pertinentes, redondantes ou fortement liées.
* Fonctionnalité sélection diminue hello nombre de fonctionnalités, ce qui rend le processus d’apprentissage du modèle hello plus efficace. Cela est particulièrement important pour les apprenants sont tootrain coûteuse telles que les machines à vecteurs de support.

Bien que la sélection des fonctionnalités cherche à nombre de hello tooreduce de fonctionnalités de modèle de hello tootrain hello jeu de données utilisé, il n’est pas généralement appelés terme de hello tooby *réduction de dimensionnalité.* Méthodes de sélection de fonctionnalité extraire un sous-ensemble de fonctionnalités d’origine dans les données de salutation sans les modifier.  Méthodes de réduction de dimensionnalité employant ingénierie des fonctionnalités qui peuvent transformer les fonctionnalités d’origine hello et donc de les modifier. Parmi les exemples de méthodes de réduction de la dimensionnalité, on peut noter l’analyse du composant principal, l’analyse canonique des corrélations et la décomposition en valeurs uniques.

L’une des méthodes de sélection de caractéristiques de catégorie largement appliquée dans un contexte supervisé est la sélection de caractéristiques par filtrage. Lors de l’évaluation de corrélation hello entre chaque attribut cible de fonctionnalité et de hello, ces méthodes s’appliquent à un tooassign mesure statistique une fonctionnalité tooeach de score. Hello fonctionnalités sont classées par score hello, qui vous permet de seuil de hello tooset pour conserver ou de suppression d’une fonctionnalité spécifique. Corrélation de Pearson, informations réciproques et test de Khi-deux hello sont des exemples de mesures statistiques de hello utilisés dans ces méthodes.

Azure Machine Learning Studio fournit des modules pour la sélection des caractéristiques. Comme indiqué dans la figure suivante de hello, ces modules sont [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] et [analyse discriminante linéaire de Fisher] [ fisher-linear-discriminant-analysis].

![Exemple de sélection de caractéristiques](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Par exemple, utiliser hello [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] module avec l’exemple d’exploration de données de texte hello décrite précédemment. Supposons que vous souhaitiez toobuild un modèle de régression après avoir créé un ensemble de 256 fonctionnalités via hello [Feature Hashing] [ feature-hashing] module et cette variable de réponse hello est **Col1**et représente un livre passer en revue l’évaluation allant de 1 too5. Définissez **méthode de notation des fonctionnalités** trop**de corrélation de Pearson**, **colonne cible** trop**Col1**, et **souhaité du nombre de fonctionnalités** trop**50**. module de Hello [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] puis génère un jeu de données contenant des 50 fonctionnalités avec l’attribut cible de hello **Col1**. Voici de Hello figure montre les flux de hello de cette expérience, hello des paramètres d’entrée.

![Exemple de sélection de caractéristiques](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Hello figure suivante illustre jeux de données résultant hello. Chaque fonctionnalité est transformée en fonction de hello de corrélation de Pearson entre lui-même et hello attribut cible **Col1**. les fonctions Hello avec les scores les plus élevés sont conservées.

![Jeux de données avec sélection de caractéristiques par filtrage](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Hello figure suivante présente hello scores correspondants de fonctionnalités de hello sélectionné.

![Scores des caractéristiques sélectionnées](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

En appliquant cette [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] module, les fonctionnalités sont sélectionnées, car ils ont hello la plupart des fonctionnalités en corrélation avec la variable cible de hello 50 de 256 **Col1** selon hello méthode de calcul de score **de corrélation de Pearson**.

## <a name="conclusion"></a>Conclusion
Ingénierie de fonctionnalité et de sélection de fonctionnalités sont deux étapes réalisées fréquemment les données d’apprentissage tooprepare hello lors de la création d’un modèle d’apprentissage. Normalement, l’ingénierie de fonctionnalité est appliqué première toogenerate des fonctionnalités supplémentaires, et puis étape de sélection de fonctionnalités hello est effectuée tooeliminate non pertinente, redondant ou des fonctionnalités hautement corrélées.

Il n’est pas toujours nécessairement sélection de fonctionnalité ou de l’équipe d’ingénierie de fonctionnalité tooperform. Si elle est nécessaire dépend des données hello ou rassembler, algorithme hello que vous choisissez, et hello l’objectif de l’expérience de hello.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
