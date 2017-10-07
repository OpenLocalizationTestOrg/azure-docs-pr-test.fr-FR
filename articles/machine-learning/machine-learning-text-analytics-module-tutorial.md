---
title: "les modèles aaaCreate texte analytique dans Azure Machine Learning Studio | Documents Microsoft"
description: "Comment analytique de texte toocreate modèles dans Azure Machine Learning Studio à l’aide de modules pour le texte de prétraitement, N-grammes ou la fonction de hachage"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Créer des modèles d’analyse de texte dans Azure Machine Learning Studio
Vous pouvez utiliser Azure Machine Learning toobuild et opérationnaliser les modèles de texte analytique. Ces modèles peuvent, par exemple, vous aider à résoudre des problèmes d’analyse de sentiments ou de classification de document.

Dans une expérience d’analyse de texte, vous devez généralement :

1. nettoyer et pré-traiter un jeu de données de texte ;
2. extraire des vecteurs de fonctions numériques du texte pré-traité ;
3. former le modèle de classification ou de régression ;
4. Évaluer et valider le modèle de hello
5. Déployer hello modèle tooproduction

Dans ce didacticiel, vous allez vous familiariser avec ces étapes au cours de l’exploration d’un modèle d’analyse de sentiments à l’aide d’un jeu de données Amazon Book Reviews (consultez l’article scientifique « Biographies, Bollywood, Boom-boxes and Blenders: Domain Adaptation for Sentiment Classification » de John Blitzer, Mark Dredze et Fernando Pereira ; Association of Computational Linguistics (ACL), 2007). Ce jeu de données se compose de notes de critiques de livres (1-2 ou 4-5) et d’un texte de forme libre. score de révision toopredict hello est Hello objectif : faible (1 - 2) ou grande (4-5).

Vous trouverez les expériences traitées dans ce didacticiel dans la galerie Cortana Intelligence :

[Predict Book Reviews](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Predict Book Reviews - Predictive Experiment](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>Étape 1 : Nettoyer et pré-traiter un jeu de données de texte
Nous commençons hello expérience en divisant les scores de révision hello en problème de hello tooformulate des compartiments faible et élevée par catégorie comme classification à deux classes. Nous utilisons les modules [Modifier les métadonnées](https://msdn.microsoft.com/library/azure/dn905986.aspx) et [Regrouper les valeurs catégoriques](https://msdn.microsoft.com/library/azure/dn906014.aspx).

![Créer une étiquette](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

Ensuite, nous clean à l’aide du texte hello [prétraiter le texte](https://msdn.microsoft.com/library/azure/mt762915.aspx) module. Hello nettoyage réduit bruit hello hello DataSet, vous permet de recherchez des fonctionnalités les plus importantes hello et améliorez hello précision du modèle final de hello. Nous supprimons les mots vides (mots courants tels que « le » ou « un ») et les chiffres, caractères spéciaux, caractères en double, adresses de messagerie et URL. Nous également convertir hello texte toolowercase lemmatize les mots hello et détecter des limites de phrases puis indiquées par « ||| « symbole dans le texte prétraitée.

![Pré-traiter le texte](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

Que se passe-t-il si vous souhaitez toouse une liste de mots vides personnalisée ? Vous pouvez la transmettre en tant qu’entrée facultative. Vous pouvez également utiliser des sous-chaînes tooreplace expression régulière syntaxe personnalisées c# et supprimer des mots en partie du message : noms verbes et adjectifs.

Une fois hello prétraitement terminée, nous fractionner les données de hello en train et ensembles de tests.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>Étape 2 : Extraire des vecteurs de fonctions numériques du texte pré-traité
toobuild un modèle pour les données de texte, vous devez en général le texte de forme libre tooconvert en vecteurs de caractéristiques numériques. Dans cet exemple, nous utilisons [extraire des fonctionnalités de N-grammes à partir du texte](https://msdn.microsoft.com/library/azure/mt762916.aspx) format toosuch des données de texte module tootransform hello. Ce module prend une colonne de mots séparés par des espaces blancs et compile un dictionnaire de mots, ou N-grammes de mots, qui apparaissent dans votre jeu de données. Ensuite, il compte le nombre de fois où chaque mot, ou N-gramme, apparaît dans chaque enregistrement et crée des vecteurs de fonction à partir de ce décompte. Dans ce didacticiel, nous avons défini too2 de taille de N-grammes, notre vecteurs de caractéristiques inclure des mots ou combinaisons de deux mots suivants.

![Extraire les N-grammes](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

Nous appliquons TF * IDF (terme fréquence Inverse Document Frequency) pondération on-grammes compte. Cette approche ajoute des poids des mots qui apparaissent fréquemment dans un seul enregistrement, mais sont rares sur hello tout jeu de données. Les autres options incluent la pondération binaire, TF et graphique.

Ces fonctionnalités de texte ont souvent une dimensionnalité élevée. Par exemple, si votre corpus comporte 100 000 mots uniques, votre espace de fonctionnalité compte 100 000 dimensions, ou plus si des N-grammes sont utilisés. module d’extraire les fonctionnalités de N-grammes Hello vous donne un ensemble de la dimensionnalité de hello tooreduce options. Vous pouvez choisir les mots tooexclude une valeur ajoutée significative prédictive toohave court ou long, ou rare trop ou trop fréquents. Dans ce didacticiel, nous excluons les N-grammes qui apparaissent dans moins de 5 enregistrements ou dans plus de 80 % des enregistrements.

En outre, vous pouvez utiliser tooselect de sélection de fonctionnalité que ces fonctionnalités hello plus corrélées avec votre cible de prédiction. Nous utilisons des fonctionnalités de 1000 de tooselect de sélection de fonctionnalité du Khi-deux. Vous pouvez afficher le vocabulaire hello de mots sélectionnés ou N-grammes en cliquant sur la sortie de droite hello du module d’extraction N-grammes.

En tant qu’une autre approche toousing extraire les fonctionnalités de N-grammes, vous pouvez utiliser le module de fonction de hachage. Notez cependant que le module [Hachage de fonctionnalité](https://msdn.microsoft.com/library/azure/dn906018.aspx) ne possède pas de capacité de sélection de fonctionnalité intégrée, ou pondération TF*IDF.

## <a name="step-3-train-classification-or-regression-model"></a>Étape 3 : Former le modèle de classification ou de régression
Maintenant le texte hello a été transformé toonumeric les colonnes de fonctionnalités. Hello dataset contient toujours les colonnes de type chaîne à partir des étapes précédentes, pour utiliser sélectionner les colonnes dans le jeu de données tooexclude les.

Nous utilisons ensuite [Two-Class Logistic Regression](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict notre cible : révision élevé ou faible score. À ce stade, problème d’analytique hello texte a été transformé en un problème de classification régulière. Vous pouvez utiliser les outils de hello disponibles dans Azure Machine Learning tooimprove hello modèle. Par exemple, vous pouvez expérimenter toofind classifieurs différents résultats précise comment ils donnent ou utilisent hyperparameter réglage de précision de hello tooimprove.

![Apprentissage et Notation](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>Étape 4 : Calcul du Score et valider le modèle de hello
Comment validerait formé hello ? Nous il évaluer hello test dataset et évaluer la précision de hello. Toutefois, le modèle de hello appris vocabulaire hello de N-grammes et leurs poids à partir du jeu de données d’apprentissage hello. Par conséquent, que nous devons utiliser ce vocabulaire et les poids lors de l’extraction des fonctionnalités à partir des données de test, en tant que nouveau et non vocabulaire de hello toocreating. Par conséquent, nous ajoutons toohello de module d’extraire les fonctionnalités de N-grammes score branche de l’expérience de hello, connecter hello sortie vocabulaire à partir de la branche de l’apprentissage et définir le mode de vocabulaire hello tooread uniquement. Nous également désactiver le filtrage de hello de N-grammes par la fréquence en définissant une instance de too1 minimale hello et too100 maximale % et désactiver la sélection de fonctionnalité hello.

Une fois hello colonne de texte dans le test de données ont été transformées toonumeric les colonnes de fonctionnalités, nous exclure chaîne hello comme les colonnes à partir des étapes précédentes dans la branche de formation. Nous utilisons ensuite des prédictions de Score Model module toomake et précision de modèle Evaluate module tooevaluate hello.

## <a name="step-5-deploy-hello-model-tooproduction"></a>Étape 5 : Déployer hello modèle tooproduction
modèle de Hello est presque prêt toobe déployé tooproduction. S’il est déployé en tant que service web, il accepte la chaîne de texte de forme libre comme entrée et retourne une prévision « élevée » ou « faible ». Il utilise hello appris N-grammes vocabulaire tootransform hello texte toofeatures et formé le modèle de régression logistique toomake une prédiction à partir de ces fonctionnalités. 

tooset d’expérience prédictive de hello, nous avons tout d’abord enregistrer vocabulaire de N-grammes hello en tant que jeu de données et hello formé le modèle de régression logistique à partir de la branche de formation hello d’expérimentation de hello. Ensuite, nous enregistrer expérience hello à l’aide de « Enregistrer sous » toocreate un graphique d’expérience pour une expérience prédictive. Nous supprimer le module de données fractionnées hello et branche de formation hello à partir de l’expérience de hello. Nous connectons vocabulaire de N-grammes hello précédemment enregistré et modèle tooExtract N-grammes fonctionnalités et modules du modèle de Score, respectivement. Nous avons également supprimer module d’évaluer le modèle hello.

Nous sélectionner les colonnes à insérer dans le module de jeu de données avant la colonne d’étiquette de texte de prétraitement module tooremove hello et désélectionnez l’option « Ajouter score colonne toodataset » dans le Module de Score. De cette façon, service web de hello ne demande pas d’étiquette hello il essaye toopredict et n’affiche pas les fonctionnalités d’entrée de hello en réponse.

![Expérience prédictive](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Nous avons à présent une expérience qui peut être publiée en tant que service web et appelée à l’aide des API requête-réponse ou exécution de lot.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les modules d’analyse de texte à partir de la [documentation MSDN](https://msdn.microsoft.com/library/azure/dn905886.aspx).

