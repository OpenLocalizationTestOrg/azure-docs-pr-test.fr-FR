---
title: "Importation de données dans Machine Learning Studio | Microsoft Docs"
description: "Découvrez comment importer vos données Azure Machine Learning Studio depuis différentes sources de données. Découvrez quels types de données et quels formats de données sont pris en charge."
keywords: "importer des données, format de données, types de données, sources de données, données d’apprentissage"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: garye;bradsev
ms.openlocfilehash: eb22f516f298df9396ca809acaa9c8cb62589c2a
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/01/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Importation de vos données d’apprentissage Azure Machine Learning Studio depuis différentes sources de données
Pour utiliser vos propres données dans Machine Learning Studio afin de développer et de tester une solution d'analyse prédictive, vous pouvez : 

* télécharger par avance les données d’un **fichier local** sur votre disque dur pour créer un module de jeu de données dans votre espace de travail
* accéder aux données à partir d’une des nombreuses **sources de données en ligne** pendant que votre expérience s’exécute à l’aide du module [Importer des données][import-data] 
* utiliser les données d’une autre **expérience** Azure Machine Learning enregistrée en tant que jeu de données
* utiliser les données depuis une **base de données SQL Server** locale

Chacune de ces options est décrite dans l’une des rubriques du menu ci-dessous. Ces rubriques montrent comment importer des données à partir de différentes sources afin de les utiliser dans Machine Learning Studio. 

[!INCLUDE [import-data-into-aml-studio-selector](../../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Un certain nombre d’exemples de jeux de données sont disponibles dans Machine Learning Studio et vous pouvez les utiliser comme données de formation. Pour plus d’informations, consultez [Utilisation des exemples de jeux de données dans Azure Machine Learning Studio](use-sample-datasets.md).
> 
> 

Cette rubrique d’introduction traite également de la préparation des données afin de les utiliser dans Machine Learning Studio, et décrit les formats et les types de données pris en charge. 

> [!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Préparation des données à utiliser dans Azure Machine Learning Studio
Machine Learning Studio est conçu pour travailler avec des données tabulaires ou rectangulaires, comme des données texte délimitées ou structurées à partir d’une base de données, bien que dans certains cas des données non rectangulaires puissent être utilisées.

Il est préférable que vos données soient relativement nettoyées. Autrement dit, vous devez régler les problèmes tels que des chaînes sans guillemet avant de télécharger les données dans votre expérience.

Toutefois, des modules de Machine Learning Studio permettent d’effectuer certaines manipulations de données dans votre expérience. En fonction des algorithmes d’apprentissage automatique que vous allez utiliser, vous devrez décider comment gérer les problèmes structurels des données tels que des valeurs manquantes et des données fragmentées. Certains modules existent pour vous aider à régler ces problèmes. Rechercher dans la section **Transformation des données** de la palette des modules ceux qui exécutent ces fonctions.

À tout moment dans votre expérience, vous pouvez voir ou télécharger les données qui sont générées par un module en cliquant sur le port de sortie. En fonction du module, différentes options de téléchargement sont disponibles. Vous pouvez également afficher les données dans votre navigateur web dans Machine Learning Studio.

## <a name="data-formats-and-data-types-supported"></a>Formats et types de données pris en charge
Vous pouvez importer un certain nombre de types de données dans votre expérience, selon le mécanisme que vous utilisez pour importer les données et l’emplacement d’où elles proviennent :

* Texte brut (.txt)
* Comma-separated values (CSV) avec un en-tête (.csv) ou sans (. nh.csv)
* Tab-separated values (TSV) avec un en-tête (.tsv) ou sans (. nh.tsv)
* Fichier Excel
* Table Azure
* Table Hive
* Base de données SQL
* Valeurs OData
* Données SVMLight (.svmlight) (voir la [définition SVMLight](http://svmlight.joachims.org/) pour les informations relatives au format)
* Données Attribute Relation File Format (ARFF) (.arff) (voir la [définition ARFF](http://weka.wikispaces.com/ARFF) pour les informations relatives au format)
* Fichier zip (.zip)
* Fichier d’espace de travail ou d’objet R (.RData)

Si vous importez des données dans un format tel que ARFF qui inclut des métadonnées, Machine Learning Studio utilise ces métadonnées pour définir le titre et le type de données de chaque colonne.

Si vous importez des données dans des formats tels que TSV ou CSV qui n’incluent pas ces métadonnées, Machine Learning Studio déduit le type de données de chaque colonne en échantillonnant les données. Si les données aussi n’ont pas non plus de titre de colonne, Machine Learning Studio fournit des noms par défaut.

Vous pouvez spécifier de manière explicite ou modifier les titres et les types de données pour les colonnes à l’aide de [Modifier les métadonnées][edit-metadata].

Voici les **types de données** reconnus par Machine Learning Studio :

* String
* Integer
* Double
* Boolean
* DateTime
* TimeSpan

Machine Learning Studio utilise un type de données interne appelé ***Table de données*** pour passer des données entre les modules. Vous pouvez convertir de manière explicite vos données dans un format de table de données à l’aide du module [Convertir en jeu de données][convert-to-dataset].

Tout module qui accepte d'autres formats que la table de données convertira silencieusement les données de la table de données avant de les passer au module suivant.

Au besoin, vous pouvez convertir à nouveau le format de la table de données au format CSV, TSV, ARFF ou SVMLight à l'aide d'autres modules de conversion.
Recherchez dans la section **Conversion des formats de données** de la palette des modules ceux qui exécutent ces fonctions.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
