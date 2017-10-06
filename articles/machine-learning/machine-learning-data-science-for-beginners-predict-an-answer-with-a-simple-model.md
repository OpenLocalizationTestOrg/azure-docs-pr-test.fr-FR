---
title: "aaaPredict une réponse avec un modèle de régression simple - Azure Machine Learning | Documents Microsoft"
description: "Comment toocreate une régression simple modèle toopredict un prix de Science des données pour les débutants vidéo 4. Comprend une régression linéaire avec des données cibles."
keywords: "créer un modèle,modèle simple,prédiction de prix,modèle de régression simple"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>Prédire une réponse à l’aide d’un modèle simple
## <a name="video-4-data-science-for-beginners-series"></a>Vidéo 4 : série Science des données pour les débutants
Découvrez comment toocreate un toopredict de modèle de régression simple hello prix de losange dans la Science des données pour les débutants vidéo 4. Nous allons dessiner un modèle de régression avec des données cibles.

hello tooget meilleur parti de série de hello, regardez les. [Atteindre liste toohello de vidéos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>Autres vidéos de cette série
*Pour la science des données pour les débutants* est une science de toodata d’introduction rapide à cinq courtes vidéos.

* Vidéo 1 : [hello 5 questions réponses de science des données](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 s)*
* Vidéo 2 : [Vos données sont-elles prêtes pour la science des données ?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sec)*
* Vidéo 3 : [Poser une question à laquelle les données permettent de répondre](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*
* Vidéo 4 : Prédire une réponse à l’aide d’un modèle simple
* Vidéo 5 : [copier la recherche de données d’autres personnes travail toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 s 18 min)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>Transcription : Prédire une réponse à l’aide d’un modèle simple
Bienvenue dans toohello quatrième vidéo Bonjour série de « Science des données pour les débutants ». Dans cette vidéo, nous allons générer un modèle simple et établir une prévision.

Un *modèle* est un scénario simplifié de nos données. Je vais vous montrer ce que cela signifie.

## <a name="collect-relevant-accurate-connected-enough-data"></a>Collecter assez de données pertinentes, précises et connectées
Disons que je veux tooshop pour un losange. J’ai un anneau qui appartenait grand-mère toomy avec un paramètre pour un losange 1,35 accent circonflexe, et je veux tooget une idée de quel sera le coût. Prendre un bloc-notes et du stylet dans le magasin de bijoux hello et écrire vers le bas prix hello de tous les cas de hello et combien ils Peser dans nombre de carats losanges hello. À compter de hello premier losange - nombre de 1,01 carats sa et $7,366.

Maintenant, je passent par et cela pour hello tous les autres losanges dans le magasin de hello.

![Colonnes de données des diamants](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

Notez que notre liste comprend deux colonnes. Chaque colonne a un attribut différent (poids en carats et prix) et chaque ligne est un point de données qui représente un diamant unique.

Nous venons de créer un petit jeu de données : une table. Notez qu’elle répond à nos critères de qualité :

* les données de salutation sont **pertinentes** -poids est définitivement connexe tooprice
* Il a **précis** -nous à double contrôle prix hello que nous écrire vers le bas
* Elles sont **connectées** (toutes les entrées du tableau sont renseignées)
* Et, comme nous allons le voir, il a **suffisamment** données tooanswer notre question

## <a name="ask-a-sharp-question"></a>Poser une question précise
Maintenant nous allons poser votre question de façon AIGUE : « quel sera le coût toobuy un losange 1,35 ACCENT CIRCONFLEXE ? »

Notre liste n’a pas un losange 1,35 accent circonflexe, afin que nous allons reste hello toouse notre tooget données un toohello répondre à la question.

## <a name="plot-hello-existing-data"></a>Tracer des données existantes de hello
Hello première chose que nous allons faire est de dessiner une ligne horizontale de numéro, appelée un axe, le poids de hello toochart. plage Hello de poids de hello étant too2 0, nous allons dessiner une ligne qui couvre de plage et placer les graduations de chaque accent circonflexe moitié.

Ensuite nous dessiner un prix de hello toorecord axe vertical et connectez-la axe horizontal de poids de toohello. Il sera exprimé en dollars. Nous disposons maintenant d’un ensemble d’axes de coordonnées.

![Axes des poids et des prix](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

Nous êtes continu tootake ces données et les convertir en un *nuage*. Il s’agit d’un excellent moyen toovisualize numériques jeux de données.

Pour le premier point de données hello, nous se rendre compte une ligne verticale au nombre de carats 1,01. Puis nous visualisons une ligne horizontale à 7 366 $. Nous dessinons un point à l’endroit où elles se rencontrent. Il représente le premier diamant.

Maintenant nous passent par chaque losange dans cette liste et hello même chose. Lorsque nous en avons terminé, voici ce que nous obtenons : un ensemble de points représentant chacun un diamant.

![nuage de points](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Dessiner modèle hello via des points de données hello
Si vous examinez squint et points de hello, collection de hello ressemble à une ligne floue fat. Nous pouvons prendre notre marqueur et tracer une ligne droite.

En dessinant une ligne, nous avons créé un *modèle*. Considérer comme prenant réel hello et de dessin animé simpliste de version de celui-ci. Maintenant, personnage de hello est incorrect - ligne de hello ne passe pas tous les points de données hello. Mais il s’agit d’une simplification utile.

![Ligne de régression linéaire](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

fait de Hello que tous les points de hello ne passent pas exactement par ligne de hello est OK. Les chercheurs de données expliquent ce à dire qu’il existe des modèle hello - ligne de hello - et ensuite chaque point certaines *bruit* ou *variance* associé. Il est hello sous-jacent relation parfaite, et est au cœur des, réel Bonjour qui ajoute le bruit et incertitude.

Étant donné que nous essayons de question de hello tooanswer *combien ?* cela s’appelle un *régression*. Et comme nous utilisons une ligne droite, c’est une *régression linéaire*.

## <a name="use-hello-model-toofind-hello-answer"></a>Utiliser la réponse de hello hello modèle toofind
Maintenant, nous disposons d’un modèle et nous lui posons notre question : combien coûte un diamant de 1,35 carat ?

tooanswer votre question, nous se rendre compte du nombre de carats 1,35 et dessiner une ligne verticale. Lorsqu’il dépasse la ligne de modèle de hello, nous se rendre compte un axe de dollar toohello ligne horizontale. Elle atteint 10 000. Et voilà ! Réponse de hello : un losange accent circonflexe 1,35 coûte environ 10 000 $.

![Trouver les réponses hello sur le modèle de hello](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>Créer un intervalle de confiance
Il est naturel toowonder quel degré de précision est de prédiction. Il est utile tooknow si losange d’accent circonflexe 1,35 hello sera très proche trop 10 000$, ou un lot supérieur ou inférieur. toofigure cette, établissons une enveloppe hello de régression qui inclut la plupart des points de hello. Cette enveloppe est appelée notre *intervalle de confiance*: nous sommes assez avec la certitude que le prix se situent dans cette enveloppe, car dans hello passée la plupart d'entre elles ont. Nous pouvons dessiner deux lignes horizontales plus à partir de la ligne d’accent circonflexe 1,35 hello intersection haut de hello et en bas de hello qu’elle contient.

![intervalle de confiance](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

Maintenant nous pouvons formulé sur notre intervalle de confiance : nous pouvons dire en toute confiance que le prix hello de losange 1,35 accent circonflexe est environ $ 10 000 - mais il peut être aussi faible que 8 000 $ et il peut être aussi élevée que 12 000 $.

## <a name="were-done-with-no-math-or-computers"></a>Nous avons terminé, sans mathématiques ni ordinateur
Nous ne les chercheurs de données paiements toodo, et nous l’avons fait simplement en dessinant :

* Nous avons posé une question à laquelle il était possible de répondre avec des données
* Nous avons créé un *modèle* à l’aide de la *régression linéaire*
* Nous avons fait une *prédiction* et l’avons affinée avec un *intervalle de confiance*

Et nous n’utilisez pas toodo mathématique ou ordinateurs il.

Maintenant, si nous disposions de plus d’informations telles que...

* Hello coupe de losange de hello
* variantes de couleur (comment fermer en forme de losange hello est toobeing blanc)
* nombre de Hello d’inclusions de losange de hello

...nous aurions plus de colonnes. Dans ce cas, les mathématiques se révèlent utiles. Si vous avez plus de deux colonnes, il est points toodraw dur sur papier. mathématique de Hello vous permet de placer la ligne ou que les données tooyour plan très bien.

Et, si nous avions deux mille ou deux millions de diamants au lieu de quelques uns, ce travail peut être réalisé beaucoup plus rapidement avec un ordinateur.

Aujourd'hui, nous avons vu comment toodo la régression linéaire et nous effectuées une prédiction à l’aide de données.

Être vraiment toocheck out hello autres vidéos de « Données scientifiques pour les débutants » à partir de Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Étapes suivantes
* [Menez une première expérience de science des données avec Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtenir une présentation tooMachine de formation sur Microsoft Azure](machine-learning-what-is-machine-learning.md)
