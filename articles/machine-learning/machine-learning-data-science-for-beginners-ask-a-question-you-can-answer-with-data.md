---
title: "aaaAsk une question d’une question - problèmes de science des données - Azure Machine Learning | Documents Microsoft"
description: "Découvrez comment tooformulate une science des données aigu question dans la Science des données pour les débutants 3 vidéo. Inclut une comparaison des questions de classification et de régression."
keywords: "problèmes de science des données,questions de science des données, formuler des questions,questions de régression,questions de classification,question précise"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Poser une question à laquelle les données permettent de répondre
## <a name="video-3-data-science-for-beginners-series"></a>Vidéo 3 : série Science des données pour les débutants
Découvrez comment tooformulate un problème de science des données dans une question dans la Science des données pour les débutants 3 vidéo. Cette vidéo inclut une comparaison des questions faisant appel aux algorithmes de classification et de régression.

hello tooget meilleur parti de série de hello, regardez les. [Atteindre liste toohello de vidéos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Autres vidéos de cette série
*Pour la science des données pour les débutants* est une science de toodata d’introduction rapide à cinq courtes vidéos.

* Vidéo 1 : [hello 5 questions réponses de science des données](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 s)*
* Vidéo 2 : [Vos données sont-elles prêtes pour la science des données ?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sec)*
* Vidéo 3 : Poser une question à laquelle les données permettent de répondre
* Vidéo 4 : [Prédire une réponse à l’aide d’un modèle simple](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*
* Vidéo 5 : [copier la recherche de données d’autres personnes travail toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 s 18 min)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>Transcription : Poser une question à laquelle les données permettent de répondre
Bienvenue dans le toohello vidéo troisième série de hello « Science des données pour les débutants. »  

Dans celle-ci, nous allons vous donner des conseils pour formuler une question à laquelle les données permettent de répondre.

Vous pouvez obtenir plus d’informations hors de cette vidéo, si vous regardez tout d’abord deux vidéos précédentes hello dans cette série : « la science des données de hello 5 questions peuvent répondre » et « Is vos données sont prêtes pour la science des données ? »

## <a name="ask-a-sharp-question"></a>Poser une question précise
Nous avons expliqué comment la science des données consiste à hello à l’aide de noms (également appelés catégories ou étiquettes) et numéros toopredict un tooa répondre à la question. Mais il ne peut pas être n’importe quelle question ; Il a toobe un *AIGUE question.*

Une vague question n’a pas toobe ayant obtenu une réponse avec un nom ou un nombre. Une question précise si.

Imaginons que vous avez trouvé une lampe magique renfermant un génie qui répond correctement à toutes les questions que vous lui posez. Mais il s’agit d’un genie partir, et il essaierons toomake sa réponse comme vague et prête à confusion car il en sortir. Vous souhaiteriez toopin lui vers le bas à poser une question donc étanche qu’il ne peut pas aider à mais indique l’action souhaitée tooknow.

Si vous étiez tooask une question imprécie, tels que « Que se passe-t-il toohappen avec mon stock ? », genie de hello peut répondre, « hello prix change ». C’est une réponse correcte, mais pas vraiment utile.

Mais si vous avez une question AIGUE, comme « Les prix de vente de mon stock seront semaine prochaine ? », hello genie ne peut pas aider mais vous donner un spécifique de tooask répondre et prédire un prix de vente.

## <a name="examples-of-your-answer-target-data"></a>Exemples de votre réponse : données cibles
Une fois que vous pouvez formuler votre question, vérifiez toosee si vous avez des exemples des réponses hello dans vos données.

Si votre question est « Quel sera le cours de mon action la semaine prochaine ? Ensuite, nous avons toomake que nos données incluent l’historique de cotation hello.

Si votre question est « quels voiture dans mon flotte est continu toofail tout d’abord ? » Ensuite, nous avons toomake que nos données incluent des informations sur les échecs précédents.

![Données cibles : exemples de votre réponse. Formulez une question de science des données.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Ces exemples de réponses sont appelés des cibles. Une cible est ce que nous sommes essayez toopredict sur les points de données ultérieure, s’il s’agit d’une catégorie ou un chiffre.

Si vous n’avez pas toutes les données de la cible, vous devez tooget certains. Vous ne sera pas en mesure de tooanswer votre question sans lui.

## <a name="reformulate-your-question"></a>Reformulez votre question
Parfois, vous pouvez reformuler votre tooget question une réponse plus utile.

question de Hello » est ce point de données A ou B ? » prévoit la catégorie de hello (ou nom ou l’étiquette) d’un objet. tooanswer, nous utilisons un *algorithme de classification*.

Hello question « Quelle mesure ? » ou « Combien ? » prévoit une quantité. tooanswer il nous utilisons un *algorithme de régression*.

toosee comment nous pouvons transformer, examinons question hello, « quel article est lecteur toothis plus intéressant de hello ? » Cette question appelle une prédiction d’un seul choix parmi de nombreuses possibilités, en d’autres termes, « S’agit-il de A, B, C ou D ? ». - avec un algorithme de classification.

Mais, cette question peut être tooanswer plus facile si vous reformuler en tant que « le niveau d’intérêt est chaque récit sur ce lecteur de toothis liste ? » Maintenant vous pouvez donner à chaque article un score numérique, il s’agit de l’article tooidentify facile hello score le plus élevé Il s’agit d’un reformuler de question de classification hello dans une question de régression ou combien ?

![Reformulez votre question. Question de classification et question de régression.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

Comment vous poser qu'une question est un algorithme de toowhich indice peut vous donner une réponse.

Vous constaterez que certaines familles d’algorithmes - comme hello ceux qui sont dans notre exemple de scénario de news - sont étroitement liés. Vous pouvez reformulez votre question toouse hello algorithme vous hello réponse plus utiles.

Toutefois, comme la plus importante, poser cette question AIGUE - question hello que vous pouvez répondre à des données. Et vérifiez que vous avez hello bonnes données tooanswer il.

Vous connaissez maintenant certains principes de base à observer pour poser une question à laquelle les données permettent de répondre.

Être vraiment toocheck out hello autres vidéos de « Données scientifiques pour les débutants » à partir de Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Étapes suivantes
* [Menez une première expérience de science des données avec Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtenir une présentation tooMachine de formation sur Microsoft Azure](machine-learning-what-is-machine-learning.md)
