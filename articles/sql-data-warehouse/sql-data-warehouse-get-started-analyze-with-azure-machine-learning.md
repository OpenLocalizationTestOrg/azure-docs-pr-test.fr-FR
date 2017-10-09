---
title: "aaaAnalyze des données avec Azure Machine Learning | Documents Microsoft"
description: "Utilisez toobuild d’Azure Machine Learning un modèle basé sur les données stockées dans Azure SQL Data Warehouse prédictive d’apprentissage."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Analyse des données avec Azure Machine Learning
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Ce didacticiel utilise Azure Machine Learning de toobuild un modèle basé sur les données stockées dans Azure SQL Data Warehouse prédictive d’apprentissage. Plus précisément, cela génère une campagne de marketing ciblée pour Adventure Works, magasin de vélo hello, la prédiction si un client est toobuy probablement un vélo ou non.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Composants requis
toostep dans ce didacticiel, vous devez :

* un entrepôt SQL Data Warehouse préchargé avec les exemples de données AdventureWorksDW. tooprovision, consultez [créer un entrepôt de données SQL] [ Create a SQL Data Warehouse] et choisissez les données d’exemple hello tooload. Si vous disposez déjà d’un entrepôt de données, mais sans disposer d’exemples de données, vous pouvez [charger manuellement des exemples de données][load sample data manually].

## <a name="1-get-hello-data"></a>1. Obtenir des données de hello
les données de salutation sont en mode de dbo.vTargetMail hello dans la base de données AdventureWorksDW hello. tooread ces données :

1. Connectez-vous à [Azure Machine Learning Studio][Azure Machine Learning studio], puis cliquez sur Mes expériences.
2. Cliquez sur **+NOUVEAU** et sélectionnez **Expérience vide**.
3. Entrez le nom de votre expérience : Marketing ciblé.
4. Hello de glisser **lecteur** module à partir du volet de modules hello dans la zone de dessin hello.
5. Spécifiez les détails de hello de votre base de données de l’entrepôt de données SQL dans le volet de propriétés hello.
6. Spécifiez la base de données hello **requête** tooread les données de salutation dignes d’intérêt.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Exécutez hello expérience en cliquant sur **exécuter** sous le canevas de l’expérience hello.
![Exécutez hello expérience][1]

Une fois que l’expérience de hello est terminée avec succès, cliquez sur le port de sortie hello bas hello de module de lecture hello et sélectionnez **visualiser** toosee hello importé des données.
![Afficher les données importées][3]

## <a name="2-clean-hello-data"></a>2. Données de salutation nettoyer
les données de salutation tooclean, de supprimer certaines colonnes ne sont pas pertinentes pour le modèle de hello. toodo cela :

1. Hello de glisser **Project Columns** module dans la zone de dessin hello.
2. Cliquez sur **sélecteur de colonne lancement** dans toospecify de volet de propriétés hello les colonnes que vous souhaitez toodrop.
   ![Colonnes de projet][4]
3. Excluez deux colonnes : CustomerAlternateKey et GeographyKey.
   ![Supprimer les colonnes inutiles][5]

## <a name="3-build-hello-model"></a>3. Générer le modèle de hello
Fractionnées hello données 80-20 : 80 % tootrain un modèle d’apprentissage et 20 % tootest hello modèle. Nous mettrons à utiliser des algorithmes de « Two-Class » hello pour ce problème de classification binaire.

1. Hello de glisser **fractionnement** module dans la zone de dessin hello.
2. Entrez 0,8 pour la Fraction de lignes dans le premier jeu de données sortie hello dans le volet de propriétés hello.
   ![Fractionner les données en jeu d’apprentissage et de test][6]
3. Hello de glisser **Two-Class Boosted Decision Tree** module dans la zone de dessin hello.
4. Hello de glisser **Train Model** module dans hello canevas et spécifier les entrées de hello. Ensuite, cliquez sur **sélecteur de colonne lancement** dans le volet de propriétés hello.
   * Première entrée : algorithme ML.
   * Deuxième entrée : algorithme hello tootrain des données sur.
     ![Connexion du module Train Model de hello][7]
5. Sélectionnez hello **BikeBuyer** colonne comme hello toopredict de colonne.
   ![Sélectionnez la colonne toopredict][8]

## <a name="4-score-hello-model"></a>4. Modèle de score hello
Maintenant, nous allez tester le fonctionne d’un modèle de hello sur les données de test. Nous allons comparer algorithme hello de notre choix avec un toosee autre algorithme qui offre de meilleures performances.

1. Faites glisser **Score Model** module dans la zone de dessin hello.
    Première entrée : la deuxième entrée du modèle objet d’un apprentissage : données de Test ![modèle hello de Score][9]
2. Hello de glisser **Two-Class Bayes Point Machine** dans le canevas de l’expérience hello. Nous allons comparer le fonctionne de cet algorithme de comparaison toohello Two-Class Boosted Decision Tree.
3. Copier et coller hello modules Train Model et le modèle de Score hello canevas.
4. Hello de glisser **modèle Evaluate** module dans les algorithmes de hello deux toocompare hello canevas.
5. **Exécutez** hello expérience.
   ![Exécutez hello expérience][10]
6. Cliquez sur le port de sortie hello bas hello du module de modèle Evaluate hello, puis cliquez sur visualiser.
   ![Visualiser les résultats de l’évaluation][11]

les métriques Hello fournies sont courbe ROC hello, n’oubliez pas de précision diagramme et courbe de courbes d’élévation. En examinant ces métriques, nous pouvons voir ce premier modèle hello effectué mieux que hello deuxième. toolook à hello que hello premier modèle a prédit, cliquez sur le port de sortie du modèle de Score de hello, puis cliquez sur visualiser.
![Visualiser les résultats de la notation][12]

Vous verrez que deux colonnes supplémentaires ajoutées tooyour test dataset.

* Les probabilités notées : probabilité que hello qu’un client est un acheteur potentiel.
* Étiquettes évaluées : hello classification effectuée par modèle hello : acheteur de vélo (1) ou non (0). Ce seuil de probabilité pour l’étiquetage a la valeur too50 % et peut être ajusté.

Comparaison des colonnes de hello BikeBuyer (réel) avec hello Scored Labels (prédiction), vous pouvez voir le modèle de hello degré. Dans les étapes suivantes, vous pouvez utiliser cette prédictions toomake de modèle pour les nouveaux clients et publier ce modèle comme un service web ou écrire tooSQL de retour de résultats entrepôt de données.

## <a name="next-steps"></a>Étapes suivantes
toolearn plus sur la création de modèles, d’apprentissage prédictive font référence trop[tooMachine de présentation de formation sur Azure][Introduction tooMachine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
