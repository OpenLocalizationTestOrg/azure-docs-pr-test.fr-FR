---
title: "données aaaImport dans Machine Learning Studio | Documents Microsoft"
description: "Comment tooimport vos données dans Azure Machine Learning Studio à partir de diverses sources de données. Découvrez quels types de données et quels formats de données sont pris en charge."
keywords: "importer des données, format de données, types de données, sources de données, données d’apprentissage"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Importation de vos données d’apprentissage Azure Machine Learning Studio depuis différentes sources de données
toouse vos propres données dans Machine Learning Studio toodevelop et effectuer l’apprentissage d’une solution prédictive analytique, vous pouvez : 

* Télécharger les données d’une **fichier local** avance par rapport de temps à partir de votre disque dur de toocreate un module de jeu de données dans votre espace de travail
* accéder aux données à partir d’un des nombreux **des sources de données en ligne** pendant que votre expérience est en cours d’exécution à l’aide de hello [importer des données] [ import-data] module 
* utiliser les données d’une autre **expérience** Azure Machine Learning enregistrée en tant que jeu de données
* utiliser les données depuis une **base de données SQL Server** locale

Chacune de ces options est décrite dans une des rubriques de hello dans menu hello ci-dessous. Les rubriques suivantes vous montrent comment tooimport des données à partir de ces données de diverses sources toouse dans Machine Learning Studio. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Un certain nombre d’exemples de jeux de données sont disponibles dans Machine Learning Studio et vous pouvez les utiliser comme données de formation. Pour plus d’informations sur ces, consultez [utiliser des jeux de données exemple hello dans Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).
> 
> 

Cette rubrique d’introduction explique comment utilisent des données tooget prêtes pour dans Machine Learning Studio également et décrit les formats de données et les types de données sont pris en charge. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Préparation des données à utiliser dans Azure Machine Learning Studio
Machine Learning Studio est toowork conçue avec des données rectangulaires ou tabulaires, telles que les données de texte délimité ou structuré de données à partir d’une base de données, bien que dans certains cas les données non rectangulaires peuvent être utilisées.

Il est préférable que vos données soient relativement nettoyées. Autrement dit, vous souhaiterez tootake administration problèmes tels que des chaînes non délimitées avant de télécharger les données de salutation dans votre expérience.

Toutefois, des modules de Machine Learning Studio permettent d’effectuer certaines manipulations de données dans votre expérience. En fonction des algorithmes d’apprentissage automatique hello vous allez utiliser, vous devrez peut-être toodecide vous allez gérer les problèmes structurels des données telles que des valeurs manquantes ou éparses et les modules qui peut aider. Regarder dans hello **Transformation des données** section de la palette de module hello pour les modules qui exécutent ces fonctions.

À tout moment dans votre expérience, vous pouvez afficher ou télécharger des données hello qui sont générées par un module en cliquant sur le port de sortie hello. En fonction du module de hello, options de téléchargement différentes peuvent être disponibles, ou vous pouvez être en mesure de toovisualize les données de salutation dans votre navigateur web dans Machine Learning Studio.

## <a name="data-formats-and-data-types-supported"></a>Formats et types de données pris en charge
Vous pouvez importer un nombre de types de données dans votre expérience, selon le mécanisme que vous utilisez les données tooimport et où il sera disponible à partir de :

* Texte brut (.txt)
* Comma-separated values (CSV) avec un en-tête (.csv) ou sans (. nh.csv)
* Tab-separated values (TSV) avec un en-tête (.tsv) ou sans (. nh.tsv)
* Fichier Excel
* Table Azure
* Table Hive
* Base de données SQL
* Valeurs OData
* Données de SVMLight (.svmlight) (voir hello [SVMLight définition](http://svmlight.joachims.org/) des informations de format)
* Attribut de données de Format de fichier de Relation (ARFF) (.arff) (voir hello [définition de ARFF](http://weka.wikispaces.com/ARFF) pour des informations de format)
* Fichier zip (.zip)
* Fichier d’espace de travail ou d’objet R (.RData)

Si vous importez des données dans un format tel que ARFF qui inclut des métadonnées, Machine Learning Studio utilise cet en-tête de métadonnées toodefine hello et le type de données de chaque colonne.

Si vous importez des données comme format TSV ou volume partagé de cluster qui n’inclut pas ces métadonnées, Machine Learning Studio déduit le type de données de hello pour chaque colonne en échantillonnant les données de salutation. Si les données de salutation n’ont également des en-têtes de colonnes, Machine Learning Studio fournit les noms par défaut.

Vous pouvez explicitement spécifier ou modifier hello des en-têtes et types de données pour les colonnes à l’aide de hello [modifier les métadonnées][edit-metadata].

suivant de Hello **des types de données** sont reconnus par Machine Learning Studio :

* String
* Integer
* Double
* Boolean
* DateTime
* TimeSpan

Machine Learning Studio utilise un type de données interne appelé ***Table de données*** toopass des données entre les modules. Vous pouvez explicitement convertir vos données dans un format de Table de données à l’aide de hello [convertir tooDataset] [ convert-to-dataset] module.

N’importe quel module qui accepte les formats de données Table convertira en mode silencieux hello données tooData Table avant de le transmettre toohello prochain module.

Au besoin, vous pouvez convertir à nouveau le format de la table de données au format CSV, TSV, ARFF ou SVMLight à l'aide d'autres modules de conversion.
Regarder dans hello **les Conversions de Format de données** section de la palette de module hello pour les modules qui exécutent ces fonctions.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
