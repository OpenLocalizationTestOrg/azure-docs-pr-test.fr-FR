---
title: "aaaIs vos données prêt pour la science des données ? Évaluation des données - Azure Machine Learning | Microsoft Docs"
description: "Découvrez les critères hello 4 pour toobe données prêt pour la science des données. Pour la science des données pour les débutants vidéo 2 a toohelp des exemples concrets avec version d’évaluation de la base de données."
keywords: "données pertinentes,évaluer des données,préparer les données,critères de données,données prêtes"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a>Vos données sont-elles prêtes pour la science des données ?
## <a name="video-2-data-science-for-beginners-series"></a>Vidéo 2 : série Science des données pour les débutants
Découvrez comment tooevaluate votre toomake de données qu’il répond aux critères de base toobe de prêt pour la science des données.

hello tooget meilleur parti de série de hello, regardez les. [Atteindre liste toohello de vidéos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a>Autres vidéos de cette série
*Pour la science des données pour les débutants* est une science de toodata d’introduction rapide à cinq courtes vidéos.

* Vidéo 1 : [hello 5 questions réponses de science des données](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 s)*
* Vidéo 2 : Vos données sont-elles prêtes pour la science des données ?
* Vidéo 3 : [Poser une question à laquelle les données permettent de répondre](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*
* Vidéo 4 : [Prédire une réponse à l’aide d’un modèle simple](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*
* Vidéo 5 : [copier la recherche de données d’autres personnes travail toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 s 18 min)*

## <a name="transcript-is-your-data-ready-for-data-science"></a>Transcription : Vos données sont-elles prêtes pour la science des données ?
Bienvenue dans trop « est vos données prêt pour la science des données ? » Hello deuxième vidéo dans une série de hello *Science des données pour les débutants*.  

Avant de la science des données peuvent donner hello de réponses, que vous avez toogive il certaines toowork de matières premières de haute qualité avec. Tout comme vous élaborez une pizza, une meilleure ingrédients hello hello, vous démarrez avec, hello mieux finale du produit hello. 

## <a name="criteria-for-data"></a>Critères pour les données
Par conséquent, dans les cas de hello de science des données, il existe certains ingrédients que nous devons toopull ensemble.

Nous avons besoin de données :

* Pertinentes
* Connecté
* Précises
* Suffisamment toowork avec

## <a name="is-your-data-relevant"></a>Vos données sont-elles pertinentes ?
Principe de première hello - nous devons donc les données qui ne s’applique.

![Données pertinentes et données non pertinentes - évaluation des données](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

Examinez la table de hello sur hello gauche. Nous allons remplies sept personnes en dehors des barres de Boston, mesurée leur niveau d’ALCOOLÉMIE, BattingAverage hello Red Sox dans leur dernière partie et prix hello de lait dans hello plus proche de la banque de commodité.

Il s’agit de données parfaitement légitimes. Le seul problème est qu’elles ne sont pas pertinentes. À première vue, il n’existe aucune relation évidente entre ces chiffres. Si vous avez hello de prix actuel de lait et hello BattingAverage Red Sox, il n’existe aucun moyen capables de deviner le contenu de mon alcool sang.

Examinez à présent les table hello sur hello droite. Cette fois, nous avons mesuré chaque numéro de la personne corps hello de masse et comptée des boissons que qui ont été.  Hello nombres dans chaque ligne sont désormais pertinentes tooeach autres. Si je vous a donné mon numéro de masse et hello de corps de Margaritas que j’ai dû, vous pouvez apporter une estimation à mon sang alcool contenu.

## <a name="do-you-have-connected-data"></a>Avez-vous des données connectées ?
les ingrédients suivant Hello sont données connectée.

![Données connectées et données non connectées - critères de données, données prêtes](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

Voici certaines données sur la qualité de hello de hamburgers : grille de température, le poids de GALETTES et classement dans hello local produits alimentaires magazine. Mais des décalages hello table hello sur hello gauche.

La plupart des jeux de données n’ont pas de valeurs. Il s’agit des trous toohave commun comme suit, et il existe toowork façons autour d’elles. Mais s’il existe trop de manquant, vos données commencent toolook comme cheese de la Suisse.

Si vous examinez la table de hello sur hello gauche, est donc la quantité de données manquante, il est dur toocome de tout type de relation entre les poids de température et GALETTES de grille. Il s’agit d’un exemple de données déconnectées.

table Hello sur hello droite, cependant, est plein et complète - un exemple de données connectée.

## <a name="is-your-data-accurate"></a>Vos données sont-elles précises ?
Bonjour ingrédients suivant, que nous devons est précision. Voici quatre cibles que nous souhaitons toohit avec des flèches.

![Données précises et des données inexactes - critères de données](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

Examinez cible hello dans le coin supérieur droit de hello. Nous avons un regroupement étroit droite autour des deux cercles concentriques hello. Ces données sont bien sûr précises. Curieusement, en langage hello de science des données, nos performances sur la droite de cible hello en dessous est également considérées comme exactes.

Si vous étiez toomap centre hello de ces flèches, vous verrez qu’il est très proche toohello bullseye. flèches de Hello sont réparties toutes autour de cible de hello, elles sont considérées comme imprécises, mais qu’elles sont centrées autour hello bullseye, elles sont considérées comme précises.

Examinez maintenant la cible du coin supérieur gauche hello. Ici, nos flèches sont très proches, regroupées étroitement. Elles sont précises, mais ils sont inexactes car le centre de hello est off deux cercles concentriques hello. Et, bien entendu, les flèches hello dans la cible de gauche hello sont incorrectes et imprécises. Cet archer a besoin de plus de pratique.

## <a name="do-you-have-enough-data-toowork-with"></a>Vous disposez de suffisamment toowork de données avec ?
Enfin, les ingrédients #4 - nous devons toohave suffisamment de données.

![Disposez-vous d’assez de données pour une analyse ? Évaluation des données](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

Considérez chaque point de données dans votre table comme un trait dans un dessin. Si vous avez uniquement certaines d'entre elles, la peinture de hello peut être assez floue ; la tootell dur, il est qu’il est.

Si vous ajoutez des contours plus, votre peinture démarre tooget un peu plus.

Lorsque vous avez à peine suffisamment traits, vous pouvez voir juste assez toomake certaines décisions large. Est un emplacement que j’aime toovisit ? Il y fait clair, l’eau semble propre : oui, c’est là où je vais partir en vacances.

Lorsque vous ajoutez davantage de données, hello tableau devient plus clair, et vous pouvez prendre des décisions plus détaillées. Je peux Examinez à présent hello trois hôtels sur la banque de gauche hello. Vous savez, vraiment comme fonctionnalités de l’architecture hello Hello un premier plan de hello. Allez rester, troisième étage de hello.

Avec les données pertinentes, connecté, précis, et suffisamment, nous avons tous les ingrédients hello nous devons toodo certains science des données de haute qualité.

Être vraiment toocheck out hello autres vidéos de quatre dans *Science des données pour les débutants* à partir de Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Étapes suivantes
* [Menez une première expérience de science des données avec Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtenir une présentation tooMachine de formation sur Microsoft Azure](machine-learning-what-is-machine-learning.md)
