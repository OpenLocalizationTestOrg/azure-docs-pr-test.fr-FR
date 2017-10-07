---
title: "Étape 3 : Création d’une expérience Machine Learning | Microsoft Docs"
description: "Étape 3 de hello développer la procédure pas à pas une solution prédictive : créer une nouvelle expérience de formation dans Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Étape 3 de la procédure pas à pas : création d’une expérience Azure Machine Learning
Il s’agit hello troisième étape de hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Télécharger des données existantes](machine-learning-walkthrough-2-upload-data.md)
3. **Créer une expérience**
4. [L’apprentissage et évaluer des modèles de hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Déployer le service Web de hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Accéder au service Web de hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
étape suivante de Hello dans cette procédure pas à pas est toocreate une expérience dans Machine Learning Studio qui utilise le jeu de données hello que nous téléchargés.  

1. Dans Studio, cliquez sur **+ nouveau** bas hello de fenêtre hello.
2. Sélectionnez **EXPÉRIENCE**, puis sélectionnez « Expérience vide ». 

    ![Création d'une expérience][0]

2. Par défaut de SELECT hello expérimenter nom haut hello de zone de dessin hello et renommez-la toosomething explicite.

    ![Renommer l’expérience][5]
   
   > [!TIP]
   > Il est une bonne approche en matière toofill **Résumé** et **Description** pour expérience hello Bonjour **propriétés** volet. Permettent de ces propriétés hello d’expérience de chance toodocument hello afin que toute personne qui consulte ultérieurement comprennent vos objectifs et la méthodologie.
   > 
   > ![Propriétés de l’expérience][6]
   > 
3. Dans hello module palette toohello gauche du canevas de l’expérience hello, développez **jeux de données enregistrés**.
4. Rechercher hello dataset est créé sous **mes Datasets** et faites-le glisser sur le canevas de hello. Vous trouverez également hello dataset en entrant le nom de hello Bonjour **recherche** zone située au-dessus de la palette de hello.  

    ![Ajouter l’expérience de hello dataset toohello][7]

## <a name="prepare-hello-data"></a>Préparer les données de salutation
Vous pouvez afficher hello les 100 premières lignes de données de hello et quelques informations statistiques pour l’ensemble du dataset hello : cliquez sur le port de sortie hello du jeu de données hello (hello petit cercle bas hello) et sélectionnez **visualiser**.  

Étant donné que le fichier de données hello n’était fourni avec des en-têtes de colonnes, Studio a fourni des en-têtes génériques (Col1, Col2, *etc.*). Bonne en-têtes ne sont pas essentiel toocreating un modèle, mais elles rendent toowork plus facile avec les données de salutation dans expérience de hello. En outre, lorsque nous publions finalement ce modèle dans un service web, des en-têtes de hello aider à identifier hello colonnes toohello utilisateur du service de hello.  

Nous pouvons ajouter des en-têtes de colonnes à l’aide de hello [modifier les métadonnées] [ edit-metadata] module.
Vous utilisez hello [modifier les métadonnées] [ edit-metadata] métadonnées toochange module avec un jeu de données. Dans ce cas, nous utilisons il tooprovide des noms plus conviviaux pour les en-têtes de colonne. 

toouse [modifier les métadonnées][edit-metadata], vous spécifiez tout d’abord le toomodify de colonnes (dans ce cas, tous les.) Ensuite, vous spécifiez hello action toobe est effectuée sur les colonnes (dans ce cas, la modification des en-têtes de colonne.)

1. Dans la palette de module hello, tapez « métadonnées » Bonjour **recherche** boîte. Hello [modifier les métadonnées] [ edit-metadata] apparaît dans la liste des modules de hello.

2. Cliquez et faites glisser hello [modifier les métadonnées] [ edit-metadata] module sur hello canevas et déposez-le sous le dataset hello ajouté précédemment.

3. Se connecter hello dataset toohello [modifier les métadonnées][edit-metadata]: cliquez sur le port de sortie hello du jeu de données hello (hello petit cercle bas hello du jeu de données hello), faites glisser le port d’entrée toohello [modifier les métadonnées ] [ edit-metadata] (hello petit cercle haut hello du module de hello), puis relâchez le bouton de la souris hello. module et le jeu de données hello restent connectés, même si vous soit déplacez sur la zone de dessin hello.
   
   expérience de Hello doit maintenant ressembler à ceci :  
   
   ![Ajout de Modifier les métadonnées][1]
   
   point d’exclamation Hello rouge indique que nous n’avons pas encore défini les propriétés hello pour ce module. Ce sera notre prochaine tâche.
   
   > [!TIP]
   > Vous pouvez ajouter un module de tooa de commentaire par module de hello en double-cliquant sur et la saisie de texte. Vous pouvez ainsi voir en un coup de œil quel module hello effectue dans votre expérience. Dans ce cas, double-cliquez sur hello [modifier les métadonnées] [ edit-metadata] module et type hello commentaire « ajouter des en-têtes de colonnes ». Cliquez sur n’importe où sur la zone de texte hello canevas tooclose hello. toodisplay hello commentaire, cliquez sur la flèche hello sur le module de hello.
   > 
   > ![Module Modifier les métadonnées avec un commentaire ajouté][8]
   > 
4. Sélectionnez [modifier les métadonnées][edit-metadata]et Bonjour **propriétés** toohello volet à droite de la zone de dessin hello, cliquez sur **sélecteur de colonne lancement**.

5. Bonjour **sélectionner des colonnes** boîte de dialogue, sélectionnez tous les hello lignes dans **colonnes disponibles** et cliquez sur > toomove les trop**colonnes sélectionnées**.
   boîte de dialogue Hello doit ressembler à ceci :

   ![Sélecteur de colonnes avec toutes les colonnes sélectionnées][2]

6. Cliquez sur hello **OK** case à cocher.

7. Dans hello **propriétés** volet, recherchez hello **nouveaux noms de colonnes** paramètre. Dans ce champ, entrez une liste de noms pour les colonnes de 21 hello dans dataset hello, séparés par des virgules et dans l’ordre des colonnes. Vous pouvez obtenir les noms de colonnes hello à partir de la documentation du jeu de données hello sur le site Web de hello UCI, ou pour des raisons pratiques, vous pouvez copier et coller hello suivant liste :  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   volet de propriétés Hello ressemble à ceci :
   
   ![Propriétés de Modifier les métadonnées][3]

> [!TIP]
> Si vous souhaitez que les en-têtes de colonne tooverify hello, exécutez l’expérience de hello (cliquez sur **exécuter** ci-dessous canevas de l’expérience hello). Lorsqu’il a terminé son exécution (une coche verte s’affiche sur [modifier les métadonnées][edit-metadata]), cliquez sur le port de sortie hello Hello [modifier les métadonnées] [ edit-metadata] module, puis sélectionnez **visualiser**. Vous pouvez afficher la sortie de hello de n’importe quel module Bonjour même progression hello tooview de façon des données hello via une expérience de hello.
> 
> 

## <a name="create-training-and-test-datasets"></a>Création de jeux de données d'apprentissage et de test
Nous avons besoin de certains modèles hello tootrain et certains tootest il.
Afin de l’étape suivante de hello d’expérimentation de hello, nous fractionné hello le jeu de données en deux jeux de données distincts : un pour l’apprentissage de notre modèle et l’autre pour le tester.

toodo, nous utilisons hello [données fractionnées] [ split] module.  

1. Recherche hello [données fractionnées] [ split] module, faites glisser sur la zone de dessin hello et connectez-la toohello [modifier les métadonnées] [ edit-metadata] module.

2. Par défaut, les taux de fractionnement hello est 0,5 et hello **aléatoire fractionnement** paramètre est défini. Cela signifie qu’une moitié aléatoire de données de salutation est sortie via un port de hello [données fractionnées] [ split] module et demi hello et autres. Vous pouvez ajuster ces paramètres, mais aussi hello **valeur initiale aléatoire** paramètre hello toochange fractionnée entre les jeux d’apprentissage et de données de test. Pour cet exemple, nous ne changeons rien.
   
   > [!TIP]
   > Hello propriété **Fraction de lignes Bonjour tout d’abord de sortie dataset** détermine la quantité de données de hello sortie via hello est *gauche* port de sortie. Par exemple, si vous définissez hello ratio too0.7, 70 % des données de salutation est sortie via hello gauche de port et 30 % via le port de droite hello.  
   > 
   > 

3. Double-cliquez sur hello [données fractionnées] [ split] module et entrez le commentaire hello, « fractionnement les données de test de formation/50 % ». 

Nous pouvons utiliser des sorties hello Hello [données fractionnées] [ split] comme test de données de sortie de module toutefois nous à, mais nous allons choisir toouse hello sortie gauche en tant que données d’apprentissage et hello à droite.  

Comme mentionné dans hello [étape précédente](machine-learning-walkthrough-2-upload-data.md), coût hello de classer par erreur entrées un risque élevé comme faible est cinq fois supérieur à celui de hello classer par erreur entrées un risque de crédit basse aussi élevée. tooaccount pour cela, nous générons un nouveau jeu de données qui reflète cette fonction de coût. Hello le nouveau jeu de données, chaque exemple de risque élevé est répliquée cinq fois, tandis que chaque exemple de risque faible n’est pas répliquée.   

Nous pouvons procéder à la réplication en utilisant le code R :  

1. Rechercher et faites glisser hello [Execute R Script] [ execute-r-script] module sur le canevas de l’expérience hello. 

2. Se connecter hello gauche du port de sortie de hello [données fractionnées] [ split] module toohello premier port d’entrée (« Dataset1 ») de hello [Execute R Script] [ execute-r-script] module.

3. Double-cliquez sur hello [Execute R Script] [ execute-r-script] module et entrez le commentaire hello, « Ajustement des coûts de la plage ».

4. Bonjour **propriétés** volet, supprimer le texte par défaut hello Bonjour **Script R** paramètre et entrez ce script :
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script R dans le module Execute R Script de hello][9]

Nous avons besoin de cette même opération de réplication pour chaque sortie hello toodo [données fractionnées] [ split] module afin que hello d’apprentissage et de données de test ont hello même ajustement des coûts. Hello plus simple façon toodo, il s’agit en dupliquant hello [Execute R Script] [ execute-r-script] module nous vient et sa connexion toohello autre sortie de port de hello [données fractionnées] [ split] module.

1. Avec le bouton hello [Execute R Script] [ execute-r-script] module et sélectionnez **copie**.

2. Cliquez sur le canevas de l’expérience hello et sélectionnez **coller**.

3. Faites glisser nouveau module de hello en position et puis connectez le port de sortie de droite hello Hello [données fractionnées] [ split] module toohello premier port d’entrée de ce nouveau [Execute R Script] [ execute-r-script] module. 

4. Au bas de hello du canevas de hello, cliquez sur **exécuter**. 

> [!TIP]
> copie Hello du module Execute R Script de hello contienne hello même script en tant que module d’origine de hello. Lorsque vous copiez et collez un module dans la zone de dessin hello, copie de hello conserve toutes les propriétés de hello Hello d’origine.  
> 
> 

À ce stade, notre expérience ressemble à cela :

![Adding Split module and R scripts][4]

Pour plus d’informations sur l'utilisation de scripts R dans vos expériences, consultez la page [Prolonger votre expérience avec R](machine-learning-extend-your-experiment-with-r.md).

**Ensuite : [Train et évaluer des modèles de hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
