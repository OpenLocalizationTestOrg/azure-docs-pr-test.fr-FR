---
title: "Étape 2 : télécharger des données dans une expérience Machine Learning | Microsoft Docs"
description: "Étape 2 de hello développer la procédure pas à pas une solution prédictive : téléchargement stockées les données publiques dans Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Étape de didacticiel pas à pas 2 : téléchargement de données existantes dans une expérience Azure Machine Learning
Il s’agit hello deuxième étape de hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Télécharger des données existantes**
3. [Créer une expérience](machine-learning-walkthrough-3-create-new-experiment.md)
4. [L’apprentissage et évaluer des modèles de hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Déployer le service Web de hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Accéder au service Web de hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop un modèle de prévision pour risque de crédit, nous avons besoin de données que nous pouvons utiliser tootrain et ensuite tester le modèle de hello. Cette procédure pas à pas, nous allons utiliser hello « Jeu de données UCI Statlog (données de crédit allemande) » à partir du référentiel d’apprentissage de communications unifiées Irvine hello. Vous pouvez le trouver ici :   
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

Nous allons utiliser le fichier hello nommé **german.data**. Télécharger ce fichier tooyour le disque dur local.  

Hello **german.data** dataset contient des lignes de 20 variables pour 1000 candidats passées de crédit. Ces 20 variables représentent l’ensemble du jeu de données hello de fonctionnalités (hello *vecteur de fonctionnalité*), qui fournit des caractéristiques d’identification pour chaque candidat de crédit. Une colonne supplémentaire dans chaque ligne représente un risque de crédit calculée du demandeur hello, avec les 700 candidats identifiés comme un risque de crédit basse et 300 comme un risque élevé.

site Web de Hello UCI fournit une description des attributs hello du vecteur de fonctionnalité hello pour ces données. Cela inclut des informations financières, l’historique de crédit, le statut professionnel et des informations personnelles. Une évaluation binaire a été appliquée à chaque candidat, afin d'indiquer s'il constitue un risque de crédit faible ou élevé. 

Nous utiliserons cette tootrain données un modèle prédictif analytique. Lorsque nous avons terminé, notre modèle doit être en mesure de tooaccept un vecteur de fonctionnalité pour une nouvelle personne et prédire si elle est un risque de crédit faible ou trop élevée.  

Voici une évolution intéressante. Bonjour description du jeu de données hello sur hello UCI site Web mentionne prix si nous misclassify risque de crédit d’une personne.
Si le modèle de hello prédit un risque élevé pour une personne qui est réellement un risque faible, le modèle de hello a apporté une erreur de classement.
Mais mauvaise classification inverse de hello est cinq fois plus coûteuse établissement toohello : si le modèle de hello prédit un risque de crédit faible pour une personne qui est réellement un risque élevé.

Par conséquent, nous souhaitons tootrain notre modèle afin que le coût de hello de ce type de ce dernier de mauvaise classification est cinq fois supérieur à celui de la classer par erreur entrées hello autre façon.
Un moyen simple toodo cela lorsque modèle hello dans notre expérience d’apprentissage est en dupliquant (cinq fois) les entrées qui représentent une personne disposant d’un risque élevé. Ensuite, si le modèle de hello misclassifies quelqu'un comme un risque de crédit faible lorsqu’ils sont en fait un risque élevé, hello fait le modèle cette mauvaise classification même cinq fois, une fois pour chaque doublon. Cela augmentera les coûts hello de cette erreur dans les résultats de formation hello.


## <a name="convert-hello-dataset-format"></a>Convertir le format de jeu de données hello
Hello de jeu de données d’origine utilise un format de séparées par des vide. Machine Learning Studio fonctionne mieux avec un fichier de valeurs séparées par des virgules (CSV), donc nous allons convertir le jeu de données de hello en remplaçant les espaces par des virgules.  

Il existe de nombreuses façons tooconvert ces données. Consiste à l’aide de hello commande de Windows PowerShell suivante :   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

Une autre méthode consiste à l’aide des commandes de sed hello Unix :  

    sed 's/ /,/g' german.data > german.csv  

Dans les deux cas, nous avons créé une version séparée par des virgules des données de hello dans un fichier nommé **german.csv** que nous pouvons utiliser dans notre expérience.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Télécharger hello dataset tooMachine Learning Studio
Une fois que les données de salutation a été converti tooCSV format, nous devons tooupload dans Machine Learning Studio. 

1. Page d’accueil de Machine Learning Studio ouvert hello ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Cliquez sur le menu de hello ![Menu][1] dans le coin supérieur gauche de hello de fenêtre hello, cliquez sur **Azure Machine Learning**, sélectionnez **Studio**et vous connecter.

3. Cliquez sur **+ nouveau** bas hello de fenêtre hello.

4. Sélectionnez **JEU DE DONNÉES**.

5. Sélectionnez **DEPUIS UN FICHIER LOCAL**.

    ![Ajouter un jeu de données à partir d’un fichier local][2]

6. Bonjour **télécharger un nouveau dataset** boîte de dialogue, cliquez sur **Parcourir** et recherche hello **german.csv** fichier que vous avez créé.

7. Entrez un nom pour le jeu de données hello. Pour les besoins de cette procédure, donnez-lui le nom suivant : « Données de carte de crédit allemande UCI ».

8. Pour le type de données, sélectionnez **Fichier CSV générique sans en-tête (.nh.csv)**.

9. Ajoutez la description de votre choix.

10. Cliquez sur hello **OK** case à cocher.  

    ![Télécharger le jeu de données hello][3]

Il télécharge des données de hello dans un module de jeu de données que nous pouvons utiliser dans une expérience.

Vous pouvez gérer des jeux de données que vous avez téléchargé tooStudio en cliquant sur hello **DATASETS** onglet toohello à gauche de la fenêtre de Studio hello.

![Gérer des jeux de données][4]

Pour plus d’informations sur l’importation d’autres types de données dans une expérience, consultez [Importez vos données d’apprentissage dans Azure Machine Learning Studio](machine-learning-data-science-import-data.md).

**Étape suivante : [créer une expérience](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
