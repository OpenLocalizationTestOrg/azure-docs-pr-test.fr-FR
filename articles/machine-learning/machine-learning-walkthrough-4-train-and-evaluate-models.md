---
title: "Étape 4 : Effectuer l’apprentissage et évaluer des modèles d’analyse prédictive hello | Documents Microsoft"
description: "Étape 4 Hello développer la procédure pas à pas une solution prédictive : effectuer l’apprentissage, évaluer et évaluer plusieurs modèles dans Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Procédure pas à pas, étape 4 : Effectuer l’apprentissage et évaluer des modèles d’analyse prédictive hello
Cette rubrique contient hello quatrième étape d’hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Télécharger des données existantes](machine-learning-walkthrough-2-upload-data.md)
3. [Créer une expérience](machine-learning-walkthrough-3-create-new-experiment.md)
4. **L’apprentissage et évaluer des modèles de hello**
5. [Déployer le service Web de hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Accéder au service Web de hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
Un des avantages de hello de l’utilisation d’Azure Machine Learning Studio pour la création de modèles d’apprentissage automatique est hello capacité tootry plus d’un type de modèle à la fois dans une expérience unique et comparer les résultats de hello. Ce type d’expérimentation vous aide à trouver des hello meilleure solution pour votre problème.

Dans l’expérience hello nous développons dans cette procédure pas à pas, nous créer deux différents types de modèles et ensuite comparer leur toodecide résultats score algorithme nous souhaitons toouse dans notre expérience finale.  

Nous avons le choix entre différents modèles. modèles de hello toosee disponibles, développez hello **Machine Learning** nœud dans la palette de module hello, puis développez **initialiser le modèle** et nœuds hello situé sous celui-ci. Fins hello de cette expérience, nous allons sélectionner hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] (SVM) et hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modules.    

> [!TIP]
> tooget déterminer plus facilement l’algorithme d’apprentissage mieux adapté à la problématique en particulier hello que vous essayez de toosolve, consultez [comment toochoose des algorithmes pour Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>L’apprentissage des modèles de hello

Nous allons ajouter deux hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module et [Two-Class Support Vector Machine] [ two-class-support-vector-machine] ce module Faites des essais.

### <a name="two-class-boosted-decision-tree"></a>Arbre de décision optimisé à deux classes

Tout d’abord, nous allons définir modèle d’arbre de décision augmenté de hello.

1. Recherche hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module dans la palette de module hello et faites-le glisser sur le canevas de hello.

2. Recherche hello [Train Model] [ train-model] module, faites glisser sur la zone de dessin hello et connectez-vous sortie hello Hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree]module toohello gauche d’un port d’entrée de hello [Train Model] [ train-model] module.
   
   Hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module initialise modèle générique hello et [Train Model] [ train-model] utilise les données d’apprentissage modèle de hello tootrain. 

3. Connecter la sortie de gauche hello de hello à gauche [Execute R Script] [ execute-r-script] toohello module droit d’entrée de port de hello [Train Model] [ train-model] module (nous décidé dans [étape 3](machine-learning-walkthrough-3-create-new-experiment.md) de cette procédure pas à pas toouse hello les données provenant hello gauche hello fractionnement du module de données pour l’apprentissage).
   
   > [!TIP]
   > Nous n’avez pas besoin de deux entrées de hello et une des sorties hello Hello [Execute R Script] [ execute-r-script] module pour cette expérience, donc nous pouvons les laisser détachés. 
   > 
   > 

Cette partie de l’expérience de hello ressemble maintenant à ceci :  

![Training a model][1]

Maintenant nous devons tootell hello [Train Model] [ train-model] module que nous souhaitons valeur risque de crédit de hello modèle toopredict hello.

1. Sélectionnez hello [Train Model] [ train-model] module. Bonjour **propriétés** volet, cliquez sur **sélecteur de colonne lancement**.

2. Bonjour **sélectionner une seule colonne** boîte de dialogue, tapez « risque de crédit » dans le champ de recherche hello sous **colonnes disponibles**, sélectionnez « Risque de crédit » ci-dessous et cliquez sur le bouton de flèche droite hello ( **>** ) toomove « Risque de crédit « trop**colonnes sélectionnées**. 

    ![Sélectionnez colonne de risque de crédit hello pour le module de Train Model hello][0]

3. Cliquez sur hello **OK** case à cocher.

### <a name="two-class-support-vector-machine"></a>Machine à vecteurs de support à deux classes

Ensuite, nous configurons modèle SVM de hello.  

Tout d’abord, une petite explication sur SVM. Les arbres de décision optimisés fonctionnent bien avec tout type de caractéristique. Toutefois, étant donné que le module SVM hello génère un classifieur linéaire, modèle hello qu’elle génère a erreur de test meilleures hello lorsque toutes les fonctions numériques ont hello même échelle. tooconvert numérique toutes les fonctionnalités toohello identique à l’échelle, nous utilisons une transformation « Tanh » (avec hello [Normalize Data] [ normalize-data] module). Cela transforme les numéros de plage de hello [0,1]. module SVM Hello convertit les fonctions toocategorical fonctions de chaîne et des fonctionnalités toobinary 0/1, donc nous ne devez toomanually transformer des fonctions de chaîne. En outre, nous ne voulons pas tootransform hello risque de crédit colonne (21) : il est numérique, mais il est valeur hello nous mettons formation hello toopredict de modèle, donc vous devez tooleave elle seule.  

tooset modèle SVM de hello, procédez comme hello suivant :

1. Recherche hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] module dans la palette de module hello et faites-le glisser sur le canevas de hello.

2. Avec le bouton hello [Train Model] [ train-model] module, sélectionnez **copie**, puis cliquez sur la zone de dessin hello et sélectionnez **coller**. Hello copie Hello [Train Model] [ train-model] module a hello sélection de la même colonne en tant que hello d’origine.

3. Connectez la sortie hello Hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] toohello du module reste un port d’entrée de hello deuxième [Train Model] [ train-model] module.

4. Recherche hello [Normalize Data] [ normalize-data] module et faites-le glisser sur le canevas de hello.

5. Connecter la sortie de gauche hello de hello à gauche [Execute R Script] [ execute-r-script] entrée toohello de module de ce module (Notez que le port de sortie hello d’un module peut être toomore connecté à un autre module).

6. Se connecter hello gauche du port de sortie de hello [normaliser des données] [ normalize-data] toohello module droite port d’entrée de hello deuxième [Train Model] [ train-model] module.

Cette partie de l'expérience ressemble alors à ceci :  

![Modèle de formation hello deuxième][2]  

À présent configurer hello [Normalize Data] [ normalize-data] module :

1. Cliquez sur tooselect hello [Normalize Data] [ normalize-data] module. Bonjour **propriétés** volet, sélectionnez **Tanh** pour hello **méthode de Transformation** paramètre.

2. Cliquez sur **sélecteur de colonne lancement**, ne sélectionnez « Aucuns colonnes » pour **commencer avec**, sélectionnez **Include** dans hello premier menu déroulant, sélectionnez **le type de colonne**dans hello le deuxième menu déroulant, puis sélectionnez **numérique** dans la liste déroulante de tiers hello. Spécifie que toutes les colonnes numériques hello (et numériques uniquement) sont transformés.

3. Cliquez sur hello toohello le signe plus (+) à droite de cette ligne, cette opération crée une rangée de menus déroulants. Sélectionnez **exclure** dans hello premier menu déroulant, sélectionnez **les noms de colonne** dans hello la deuxième liste déroulante et entrez « Risque de crédit » dans le champ de texte hello. Cela spécifie que cette colonne de risque de crédit hello doit être ignorée (nous devons toodo cela, car cette colonne est numérique et il sera transformé si nous n’avez pas l’exclure).

4. Cliquez sur hello **OK** case à cocher.  

    ![Sélectionnez des colonnes pour le module de normaliser les données hello][5]

Hello [Normalize Data] [ normalize-data] module est désormais ensemble tooperform une transformation Tanh sur toutes les colonnes numériques à l’exception de hello risque de crédit.  

## <a name="score-and-evaluate-hello-models"></a>Calcul du score et évaluer des modèles de hello

Nous utilisons hello test des données qui a été séparées par hello [données fractionnées] [ split] module tooscore nos modèles formés. Nous pouvons ensuite comparer les résultats hello de hello deux modèles toosee qui a généré les meilleurs résultats.  

### <a name="add-hello-score-model-modules"></a>Ajouter des modules de Score Model hello

1. Recherche hello [Score Model] [ score-model] module et faites-le glisser sur le canevas de hello.

2. Se connecter hello [Train Model] [ train-model] module qui s’est connecté toohello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] entrée gauche toohello de module port de hello [Score Model] [ score-model] module.

3. Se connecter à droite de hello [Execute R Script] [ execute-r-script] toohello de module (nos données de test) à droite d’entrée de port de hello [Score Model] [ score-model] module.

    ![Module Noter le modèle connecté][6]
   
   Hello [Score Model] [ score-model] module peut désormais tirer des informations relatives au crédit hello de hello données, exécutez-le jusqu’au modèle hello, de test et des prédictions hello de comparer les modèle hello génère par hello réel risque de crédit colonne Bonjour de données de test.

4. Copiez et collez hello [Score Model] [ score-model] module toocreate une seconde copie.

5. Connecter la sortie hello du modèle SVM hello (autrement dit, hello sortie de hello [Train Model] [ train-model] module qui s’est connecté toohello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] module) toohello port d’entrée de hello deuxième [Score Model] [ score-model] module.

6. Pour un modèle SVM de hello, nous avons toodo hello les mêmes données de test toohello transformation comme nous l’avons fait des données d’apprentissage toohello. Par conséquent, copiez et collez hello [normaliser les données] [ normalize-data] module toocreate une deuxième copie et le connecter à droite de toohello [Execute R Script] [ execute-r-script] module.

7. Connectez ensuite de sortie de gauche de hello Hello [Normalize Data] [ normalize-data] toohello module droite port d’entrée de hello deuxième [Score Model] [ score-model] module.

    ![Deux modules Noter le modèle connectés][7]

### <a name="add-hello-evaluate-model-module"></a>Ajouter hello évaluer le modèle module

tooevaluate hello deux résultats de calcul de score et de les comparer, nous utilisons un [modèle Evaluate] [ evaluate-model] module.  

1. Recherche hello [modèle Evaluate] [ evaluate-model] module et faites-le glisser sur le canevas de hello.

2. Connectez le port de sortie de hello de hello [Score Model] [ score-model] module associé hello augmentés décision arborescence modèle toohello gauche d’entrée de port de hello [modèle Evaluate] [ evaluate-model] module.

3. Se connecter hello autres [Score Model] [ score-model] toohello module droit d’entrée de port.  

    ![Module Évaluer le modèle connecté][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Exécutez hello expérience et vérifier les résultats de hello

toorun hello expérience, cliquez sur hello **exécuter** situé sous la zone de dessin hello. Cette opération peut prendre quelques minutes. Un indicateur de rotation sur chaque module indique qu’il est en cours d’exécution et ensuite une coche verte indique quand le module de hello est terminée. Lorsque tous les modules hello possèdent une coche, expérience de hello a terminé son exécution.

expérience de Hello doit maintenant ressembler à ceci :  

![Evaluating both models][3]

résultats de hello toocheck, cliquez sur le port de sortie hello Hello [modèle Evaluate] [ evaluate-model] module et sélectionnez **visualiser**.  

Hello [modèle Evaluate] [ evaluate-model] module génère une paire de courbes et les mesures qui permettent de résultats de hello toocompare de deux modèles de score hello. Vous pouvez afficher les résultats de hello en tant que courbes récepteur opérateur caractéristique (ROC), des courbes de précision et de rappel ou des courbes de courbes d’élévation. Données supplémentaires affichées incluent une matrice de confusion, les valeurs cumulées de zone hello sous la courbe de hello (AUC) et d’autres mesures. Vous pouvez modifier la valeur de seuil hello par déplacement de curseur hello gauche ou droite et voir comment il affecte ensemble hello de mesures.  

toohello à droite du graphique de hello, cliquez sur **transformée dataset** ou **transformée dataset toocompare** toohighlight Bonjour associé courbe et toodisplay Bonjour associés métriques ci-dessous. Dans légende hello pour les courbes de hello, « Transformée dataset » correspond toohello gauche d’un port d’entrée de hello [modèle Evaluate] [ evaluate-model] module - dans le cas présent, il s’agit modèle d’arbre de décision augmenté de hello. « Transformée dataset toocompare » correspond port d’entrée droite toohello - modèle SVM hello dans notre cas. Lorsque vous cliquez sur une de ces étiquettes, courbe hello pour ce modèle est mis en surbrillance et les métriques correspondant hello sont affichent, comme indiqué dans le graphique suivant de hello.  

![ROC curves for models][4]

En examinant ces valeurs, vous pouvez décider quel modèle est le plus proche toogiving que Hello de résultats que vous recherchez. Vous pouvez revenir en arrière et itérez au sein de votre expérience en modifiant les valeurs de paramètre dans des modèles différents hello. 

science de Hello et art d’interpréter ces résultats et de paramétrage des performances du modèle hello est étendue de hello en dehors de cette procédure pas à pas. Pour obtenir une aide supplémentaire, vous pouvez lire hello suivant des articles :
- [Comment tooevaluate modèle de performances dans Azure Machine Learning](machine-learning-evaluate-model-performance.md)
- [Choisissez des paramètres toooptimize vos algorithmes dans Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md)
- [Interprétation des résultats de modèle dans Azure Machine Learning](machine-learning-interpret-model-results.md)

> [!TIP]
> Chaque fois que vous exécutez expérience de hello un enregistrement de cette itération est conservée dans hello historique d’exécution. Vous pouvez afficher ces itérations et revenir tooany d'entre elles, en cliquant sur **afficher l’historique d’exécution** sous la zone de dessin hello. Vous pouvez également cliquer sur **exécuter préalable** Bonjour **propriétés** itération de toohello tooreturn volet précédant hello un est ouvert.
> 
> Vous pouvez effectuer une copie d’une itération de votre expérience en cliquant sur **SAVE AS** sous la zone de dessin hello. 
> Utiliser d’expérience hello **Résumé** et **Description** propriétés tookeep un enregistrement de ce que vous avez essayé de dans les itérations de votre expérience.
> 
> Pour en savoir plus, consultez la section [Gérer les itérations des expériences dans Microsoft Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).  
> 
> 

- - -
**Ensuite : [déployer hello web service](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
