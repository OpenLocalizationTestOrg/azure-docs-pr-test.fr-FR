---
title: "aaaUse Azure Machine Learning avec l’entrepôt de données SQL | Documents Microsoft"
description: "Didacticiel sur l’utilisation de Microsoft Azure Machine Learning avec Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Utilisation de Microsoft Azure Machine Learning avec SQL Data Warehouse
Azure Machine Learning est un service entièrement géré analytique prédictives que vous pouvez utiliser les modèles prédictifs toocreate par rapport à vos données dans l’entrepôt de données SQL et puis publier en tant que services web de prêt à consommer. Vous pouvez les principes fondamentaux d’analytique prédictive hello et apprentissage en lisant [tooMachine de présentation de formation sur Azure][Introduction tooMachine Learning on Azure].  Vous pouvez ensuite apprendre comment toocreate, l’apprentissage, évaluer et tester un modèle d’apprentissage automatique à l’aide de hello [créer expérience didacticiel][Create experiment tutorial].

Dans cet article, vous allez apprendre comment hello toodo suivant à l’aide de hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:

* Les données lues à partir de votre base de données toocreate, effectuer l’apprentissage et le score d’un modèle de prévision
* Écriture de base de données tooyour de données

## <a name="read-data-from-sql-data-warehouse"></a>Lire des données à partir de SQL Data Warehouse
Données seront lues à partir de la table Product dans la base de données AdventureWorksDW hello.

### <a name="step-1"></a>Étape 1
Démarrez une nouvelle expérience en cliquant sur + Nouveau bas hello hello fenêtre de la Machine Learning Studio, sélectionnez expérience, puis faire des essais vide. Par défaut de hello sélectionnez expérimenter nom haut hello de zone de dessin hello et renommez-la toosomething explicite, par exemple, les prédiction de prix de bicyclette.

### <a name="step-2"></a>Étape 2
Recherchez le module de lecture hello dans la palette hello des jeux de données et les modules sur gauche hello du canevas de l’expérience hello. Faites glisser le canevas de l’expérience toohello module hello.
![][drag_reader]

### <a name="step-3"></a>Étape 3 :
Sélectionnez le module de lecture hello et remplir le volet de propriétés hello.

1. Sélectionnez la base de données SQL Azure en tant que Source de données de hello.
2. Nom du serveur de base de données : nom de serveur de Type hello. Vous pouvez utiliser hello [portail Azure] [ Azure portal] toofind cela.

![][server_name]

1. Nom de la base de données : nom hello du Type de base de données sur le serveur hello vous venez de spécifier.
2. Nom du compte utilisateur Server : nom d’utilisateur de Type hello d’un compte qui dispose des autorisations d’accès pour la base de données hello.
3. Mot de passe utilisateur Server : fournir un mot de passe hello pour hello de compte d’utilisateur spécifié.
4. Accepter n’importe quel certificat du serveur : utilisez cette option (moins sûr) si vous souhaitez tooskip examiner le certificat de site hello avant de lire vos données.
5. Requête de base de données : entrez une instruction SQL qui décrit les données hello tooread. Dans ce cas, nous lira des données à partir de la table Product à l’aide de hello suivant la requête.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Étape 4
1. Exécutez hello expérience en cliquant sur Exécuter dans le canevas de l’expérience hello.
2. Fin de l’expérience de hello, module de lecture hello aura un tooindicate de coche verte a terminé avec succès. Notez également hello vous avez terminé de l’état en cours d’exécution dans le coin supérieur droit de hello.

![][run]

1. toosee hello des données importées, cliquez sur le port de sortie hello bas hello du jeu de données automobile hello et sélectionnez visualiser.

## <a name="create-train-and-score-a-model"></a>Créer, former et évaluer un modèle
Vous pouvez désormais utiliser ce jeu de données pour effectuer les opérations suivantes :

* Créer un modèle : traiter des données et définir des fonctionnalités.
* Modèle de hello train : choisissez d’appliquer un algorithme d’apprentissage
* Score et test de modèle hello : prédire nouveau prix de bicyclette

![][model]

toolearn plus en détail comment toocreate, l’apprentissage, évaluer et tester un hello d’utilisation de modèle d’apprentissage [créer expérience didacticiel][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Écrire des données tooAzure SQL Data Warehouse
Nous écrirons hello résultat ensemble tooProductPriceForecast table dans la base de données AdventureWorksDW hello.

### <a name="step-1"></a>Étape 1
Recherchez le module de Writer hello dans la palette hello des jeux de données et les modules sur gauche hello du canevas de l’expérience hello. Faites glisser le canevas de l’expérience toohello module hello.

![][drag_writer]

### <a name="step-2"></a>Étape 2
Sélectionnez le module de Writer hello et remplir le volet de propriétés hello.

1. Sélectionnez base de données SQL Azure comme Destination des données de hello.
2. Nom du serveur de base de données : nom de serveur de Type hello. Vous pouvez utiliser hello [portail Azure] [ Azure portal] toofind cela.
3. Nom de la base de données : nom hello du Type de base de données sur le serveur hello vous venez de spécifier.
4. Nom du compte utilisateur Server : nom d’utilisateur de Type hello d’un compte qui dispose des autorisations d’écriture pour la base de données hello.
5. Mot de passe utilisateur Server : fournir un mot de passe hello pour hello de compte d’utilisateur spécifié.
6. Accepter n’importe quel certificat du serveur (non sécurisé) : sélectionnez cette option si vous ne souhaitez pas certificat de hello tooview.
7. Séparées par des virgules de liste de toobe colonnes enregistré : fournir une liste de colonnes de jeu de données ou le résultat de hello que vous souhaitez toooutput.
8. Nom de table de données : spécifiez le nom hello de table de données hello.
9. Séparées par des virgules de liste de colonnes de la table de données : spécifiez toouse de noms de colonne hello dans la nouvelle table de hello. Hello les noms de colonne peuvent être différents de hello ceux qui sont dans le jeu de données source hello, mais vous devez répertorier hello même nombre de colonnes ici que vous définissez pour la table de sortie hello.
10. Nombre de lignes écrites par opération SQL Azure : vous pouvez configurer le nombre de hello de lignes écrites tooa base de données SQL en une seule opération.

![][writer_properties]

### <a name="step-3"></a>Étape 3 :
1. Exécutez hello expérience en cliquant sur Exécuter dans le canevas de l’expérience hello.
2. Fin de l’expérience de hello, tous les modules aura un tooindicate de coche verte avec succès.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
