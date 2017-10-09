---
title: "sélection aaaFeature Bonjour processus de science des données équipe | Documents Microsoft"
description: "Explique l’objectif hello de sélection de fonctionnalités et fournit des exemples de leur rôle dans le processus d’amélioration de données hello de l’apprentissage."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Sélection des fonctionnalités dans hello processus de science des données équipe (TDSP)
Cet article explique à des fins de hello de sélection de fonctionnalités et fournit des exemples de son rôle dans le processus d’amélioration de données hello de l’apprentissage. Ces exemples sont tirés d’Azure Machine Learning Studio. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Hello d’ingénierie et sélection de fonctionnalités est un composant d’hello équipe données science des processus (TDSP) décrites dans [What ' s hello processus de science des données équipe ?](data-science-process-overview.md). Ingénierie de fonctionnalité et de sélection sont les parties de hello **développer les fonctionnalités** étape Hello TDSP.

* **l’équipe d’ingénierie de fonctionnalité**: ce processus tente de toocreate des fonctionnalités pertinentes supplémentaires à partir de hello existant brutes fonctionnalités dans les données de salutation et algorithme d’apprentissage toohello tooincrease prédictif.
* **sélection des fonctionnalités**: ce processus sélectionne un sous-ensemble de clés de hello des fonctionnalités de données d’origine dans une dimensionnalité de hello tooreduce tentative de problème de formation hello.

Normalement **l’équipe d’ingénierie de fonctionnalité** est appliqué première toogenerate des fonctionnalités supplémentaires, puis hello **sélection des fonctionnalités** étape est effectuée tooeliminate hautement corrélée inutile ou redondante fonctionnalités.

## <a name="filtering-features-from-your-data---feature-selection"></a>Filtrage des caractéristiques à partir de vos données - Sélection de caractéristiques
Sélection de fonctionnalités est un processus qui est généralement appliqué pour la construction de hello de jeux de données d’apprentissage pour les tâches de modélisation prédictive comme les tâches de classification ou de régression. Hello vise tooselect un sous-ensemble de fonctionnalités hello à partir du jeu de données d’origine hello réduire ses dimensions à l’aide d’un ensemble minimal de fonctionnalités toorepresent hello maximum de variance dans les données de salutation. Ce sous-ensemble de fonctionnalités sont ensuite, hello seules fonctionnalités toobe inclus le modèle de hello tootrain. La sélection de caractéristiques a deux principaux objectifs.

* Tout d'abord, la sélection des caractéristiques augmente souvent la précision de classification en éliminant les caractéristiques non pertinentes, redondantes ou fortement liées.
* En second lieu, il diminue le nombre hello des fonctionnalités qui rend le processus d’apprentissage du modèle plus efficace. Cela est particulièrement important pour les apprenants sont tootrain coûteuse telles que les machines à vecteurs de support.

Bien que la sélection des fonctionnalités vise le nombre de hello tooreduce de fonctionnalités de modèle de hello tootrain hello dataset utilisé, il n’est pas généralement tooby référencé hello terme « réduction de dimensionnalité ». Méthodes de sélection de fonctionnalité extraire un sous-ensemble de fonctionnalités d’origine dans les données de salutation sans les modifier.  Méthodes de réduction de dimensionnalité employant ingénierie des fonctionnalités qui peuvent transformer les fonctionnalités d’origine hello et donc de les modifier. Parmi les exemples de méthodes de réduction de la dimensionnalité, on peut noter l'analyse du composant principal, l'analyse canonique des corrélations et la décomposition en valeurs uniques.

Notamment, l'une des méthodes de sélection de caractéristiques de catégorie largement appliquée dans un contexte supervisé est appelée « sélection de caractéristiques basée sur les filtres ». Lors de l’évaluation de corrélation hello entre chaque attribut cible de fonctionnalité et de hello, ces méthodes s’appliquent à un tooassign mesure statistique une fonctionnalité tooeach de score. fonctionnalités de Hello sont classées par score hello, qui peut être utilisé toohelp ensemble hello seuil pour conserver ou de suppression d’une fonctionnalité spécifique. Personne corrélation informations réciproques et test de hello Chi carré sont des exemples de mesures statistiques de hello utilisés dans ces méthodes.

Dans Azure Machine Learning Studio, des modules sont fournis pour la sélection des caractéristiques. Comme indiqué dans la figure suivante de hello, ces modules sont [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] et [analyse discriminante linéaire de Fisher] [ fisher-linear-discriminant-analysis].

![Exemple de sélection de caractéristiques](./media/machine-learning-data-science-select-features/feature-Selection.png)

Considérez, par exemple, utilisez hello Hello [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] module. Pour les besoins de hello de commodité, nous continuons toouse hello texte d’exploration de données exemple présentée ci-dessus. Supposons que nous souhaitons toobuild un modèle de régression après un ensemble de 256 fonctionnalités sont créés via hello [Feature Hashing] [ feature-hashing] module et cette variable de réponse hello est hello « Col1 » et représente un livre Passez en revue les évaluations allant de 1 too5. En définissant la « Fonctionnalité de calcul de score méthode » toobe « Corrélation de Pearson », hello « Colonne cible » toobe « Col1 » et too50 de « Nombre de fonctionnalités » hello. Puis hello module [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] génère un dataset qui contient des 50 fonctionnalités avec l’attribut cible de hello « Col1 ». Voici de Hello figure montre les flux de hello de cette expérience, hello nous venons de voir les paramètres d’entrée.

![Exemple de sélection de caractéristiques](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Hello figure suivante illustre les jeux de données obtenus hello. Chaque fonctionnalité est transformée en fonction de hello de corrélation de Pearson entre lui-même et hello l’attribut cible « Col1 ». les fonctions Hello avec les scores les plus élevés sont conservées.

![Exemple de sélection de caractéristiques](./media/machine-learning-data-science-select-features/feature-Selection2.png)

scores de Hello correspondant de fonctionnalités de hello sélectionné sont affichés dans hello figure suivante.

![Exemple de sélection de caractéristiques](./media/machine-learning-data-science-select-features/feature-Selection3.png)

En appliquant cette [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] module, 50 de 256 fonctionnalités sont sélectionnées, car ils ont hello plus les fonctionnalités corrélées avec la variable cible de hello « Col1 », en fonction de calcul de score hello méthode « Corrélation de Pearson ».

## <a name="conclusion"></a>Conclusion
Ingénierie de fonctionnalité et de sélection de fonctionnalités sont deux couramment conçu et de fonctionnalités sélectionnées accroître l’efficacité de hello Hello formation des processus qui essaie d’informations de clé de hello tooextract contenues dans les données de salutation. Ils améliorent également power hello de ces modèles tooclassify hello d’entrée de données avec précision et toopredict des résultats d’intéressent plus efficacement. Ingénierie de fonctionnalité et de sélection peuvent également combiner des toomake d’apprentissage automatique hello en plus de calculs souple. Il le fait en améliorant et réduction de plusieurs fonctionnalités hello nécessaires toocalibrate ou effectuer l’apprentissage d’un modèle. Strictement mathématique, modèle de hello hello fonctionnalités tootrain sélectionné sont un ensemble minimal de variables indépendantes qui expliquent les schémas hello dans les données de salutation et puis prédire les résultats avec succès.

Notez qu’il n’est pas toujours nécessairement sélection de fonctionnalité ou de l’équipe d’ingénierie de fonctionnalité tooperform. Si elle est nécessaire ou non dépend des données hello nous avons ou collecter, algorithme hello que prendre, et hello l’objectif de l’expérience de hello.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

