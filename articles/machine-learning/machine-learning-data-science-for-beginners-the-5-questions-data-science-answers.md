---
title: "pour la science des données aaaThe 5 questions - science des données pour les débutants - Azure Machine Learning | Documents Microsoft"
description: "Science des données pour les débutants est explique des concepts de base dans 5 courtes vidéos, en commençant par les réponses de science des données hello 5 Questions. À partir d’Azure Machine Learning."
keywords: "utiliser la science des données,débutants en science des données,science des données pour les débutants,notions de base de la science des données,questions de science des données,vidéo de sciences de données,présentation de la science des données"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a01f93ee-01eb-4afe-abbd-cfa035c119b0
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 6de0ca22556771a3044520d9ccc6771c3de78771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-for-beginners-video-1-hello-5-questions-data-science-answers"></a>Pour la science des données pour les débutants vidéo 1 : hello 5 questions réponses de science des données
Obtenir une science de toodata une introduction rapide à partir de *Science des données pour les débutants* dans cinq courtes vidéos à partir d’un chercheur de données supérieure. Ces vidéos sont simples mais utiles, que vous souhaitiez travailler sur la science des données ou collaborer avec d’autres scientifiques.

Cette première vidéo concerne les types hello de questions science des données peuvent répondre. hello tooget meilleur parti de série de hello, regardez les. [Atteindre liste toohello de vidéos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/8/player]
>
>

## <a name="other-videos-in-this-series"></a>Autres vidéos de cette série
*Pour la science des données pour les débutants* est une science toodata de présentation rapide prend environ 25 minutes au total. Regardez les cinq vidéos :

* Vidéo 1 : hello 5 questions réponses de science des données
* Vidéo 2 : [Vos données sont-elles prêtes pour la science des données ?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sec)*
* Vidéo 3 : [Poser une question à laquelle les données permettent de répondre](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*
* Vidéo 4 : [Prédire une réponse à l’aide d’un modèle simple](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*
* Vidéo 5 : [copier la recherche de données d’autres personnes travail toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 s 18 min)*

## <a name="transcript-hello-5-questions-data-science-answers"></a>Transcription : hello 5 questions réponses de science des données
Bonjour ! Bienvenue dans la série de vidéos toohello *Science des données pour les débutants*.

Recherche de données peut vous paraître intimidante, donc je présenterai hello notions de base ici sans équations ou ordinateur jargon de programmation.

Dans cette première vidéo, nous parlerons de « hello 5 questions données science des réponses. »

Science des données utilise des nombres et les noms (également connu sous les catégories ou les étiquettes) toopredict réponses tooquestions.

Cela peut vous surprendre, mais *il existe cinq questions auxquelles la science des données répond*:

* Est-ce A ou B ?
* Est-ce étrange ?
* Quelle quantité (ou combien) ?
* Comment les données sont-elles organisées ?
* Que dois-je faire ensuite ?

Un groupe spécifique de méthodes d’apprentissage automatique, appelées algorithmes, permet de répondre à ces questions.

Il est utile toothink sur un algorithme à une recette et vos données comme les ingrédients hello. Un algorithme indique comment toocombine et mélanger hello données dans l’ordre tooget une réponse. Les ordinateurs sont comme un mixeur. Ils font la plupart du travail de l’algorithme de hello hello pour vous, et ce assez rapidement.

## <a name="question-1-is-this-a-or-b-uses-classification-algorithms"></a>La question 1 (Est-ce A ou B ?) utilise des algorithmes de classification
Commençons par question de hello : soit cette A B ?

![Algorithmes de classification : est-ce A ou B ?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/classification-algorithms.png)

Cette famille d’algorithmes est appelée la classification double classe.

Elle est utile pour toute question qui n’a que deux réponses possibles.

Par exemple :

* Cette PNEU échoue dans hello miles 1 000 suivants : Oui ou non ?
* Qu’est-ce qui attire le plus les clients : un coupon de 5 $ ou une remise de 25 % ?

Cette question peut également être tooinclude rephrased plus de deux options : soit cette A ou B ou C D, etc.. ?  On parle de classification multiclasse. Elle est utile lorsque vous avez plusieurs (ou plusieurs milliers) de réponses possibles. Classification multiclasse choisit hello probablement un.

## <a name="question-2-is-this-weird-uses-anomaly-detection-algorithms"></a>La question 2 (Est-ce bizarre ?) utilise des algorithmes de détection d’anomalies
question suivante de Hello science des données peuvent répondre est : est cette étrange ? Pour répondre à cette question, on utilise une famille d’algorithmes appelée détection des anomalies.

![Algorithmes de détection d’anomalies : est-ce bizarre ?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/anomaly-detection-algorithms.png)

Si vous disposez d’une carte de crédit, vous avez déjà bénéficié de la détection des anomalies. Votre société de carte de crédit analyse vos modèles d’achat, afin qu’ils peuvent vous alerter toopossible fraude. Les frais considérés comme « étranges » peuvent être liés à un achat dans un magasin dans lequel vous ne faites normalement aucun achat ou à un achat anormalement coûteux.

Cette question peut se révéler utile dans de nombreux cas. Exemple :

* Si vous avez une voiture des jauges de pression, vous pourriez tooknow : est cette jauge de sollicitation de la lecture normale ?
* Si vous êtes analyse hello internet, vous pouvez tooknow : ce message à partir de hello internet classique ?

La détection d’anomalies signale des événements ou comportements inattendus ou inhabituels. Il donne des indices où toolook des problèmes.

## <a name="question-3-how-much-or-how-many-uses-regression-algorithms"></a>La question 3 (Quelle quantité ou combien ?) utilise des algorithmes de régression
Apprentissage permet également de prédire hello réponse tooHow beaucoup ? et la manière dont plusieurs ? famille d’algorithmes Hello qui répond à cette question est appelée régression.

![Algorithmes de régression : quelle quantité ou combien ?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/regression-algorithms.png)

Les algorithmes de régression effectuent des prédictions numériques, notamment :

* Ce que sera hello température d’être le mardi suivant ?  
* Quelles seront mes ventes au quatrième trimestre ?

Ils peuvent répondre à toute question dont la réponse est un chiffre.

## <a name="question-4-how-is-this-organized-uses-clustering-algorithms"></a>La question 4 (Comment les données sont-elles organisées ?) utilise des algorithmes de clustering
Maintenant les deux derniers questions hello sont un peu plus avancé.

Parfois, vous souhaitez que structure de hello toounderstand d’un jeu de données - comment cela organisée ? Pour cette question, vous ne disposez pas d’exemples dont vous connaissez déjà les résultats.

Il existe un grand nombre de tootease façons structure hello de données. L’une des approches est le clustering. Elle sépare les données en groupes naturels pour en simplifier l’interprétation. Avec le clustering, il n’existe pas une seule réponse.

![Algorithmes de clustering : comment les données sont-elles organisées ?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/clustering-algorithms.png)

Les exemples suivants sont des questions de clustering courantes :

* Les visionneuses comme hello mêmes types de films ?
* Les modèles d’imprimante échouent hello identique ?

En comprenant comment les données sont organisées, vous pouvez mieux comprendre (et prédire) des événements et des comportements.  

## <a name="question-5-what-should-i-do-now-uses-reinforcement-learning-algorithms"></a>La question 5 (Que dois-je faire ensuite ?) utilise des algorithmes d’apprentissage par renforcement
Hello dernière question : que dois-je faire maintenant ? - utilise une famille d’algorithmes appelée apprentissage de renforcement.

Apprentissage de renforcement a été inspiré par comment cerveau hello de rats et l’homme répond toopunishment et récompense. Ces algorithmes apprendre des résultats et décider de l’action suivante de hello.

En règle générale, l’apprentissage renforcement est adapté pour les systèmes automatisés comportant un grand nombre de toomake de petites décisions sans instructions humaine.

![Algorithmes d’apprentissage par renforcement : que dois-je faire ensuite ?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/reinforcement-learning-algorithms.png)

Les questions auxquelles il répond concernent toujours l’action à exécuter (généralement par une machine ou un robot). Voici quelques exemples :

* Si je suis un système de contrôle de température d’une maison : régler la température de hello ou laissez le champ sur lequel il est ?  
* Si je suis une voiture à conduite automatique : freiner ou accélérer au feu orange ?  
* Pour un vide robot : conservez ramasse-miettes, ou revenir en arrière toohello poste de charge ?

Les algorithmes d’apprentissage par renforcement collectent les données au fur et à mesure et apprend de ses essais et de ses erreurs.

C’est elle - science des données de hello 5 questions peuvent répondre.

## <a name="next-steps"></a>Étapes suivantes
* [Menez une première expérience de science des données avec Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtenir une présentation tooMachine de formation sur Microsoft Azure](machine-learning-what-is-machine-learning.md)
