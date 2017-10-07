---
title: "procédures pas à pas d’aaaHDInsight Spark sur Azure à l’aide de PySpark et Scala | Documents Microsoft"
description: "Exemples de hello processus de science des données équipe présentant hello utilisent de PySpark et Scala sur une analytique de prédictive toodo Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>Guides de la science des données HDInsight Spark avec PySpark et Scala sur Azure

Ces procédures pas à pas utiliser PySpark et Scala sur une analytique de prédictive toodo de cluster Azure Spark. Elles suivent les étapes hello hello processus de science des données équipe. Pour une vue d’ensemble de hello processus de science des données équipe, consultez [processus de science des données](data-science-process-overview.md). Pour une vue d’ensemble de Spark sur HDInsight, consultez [tooSpark Introduction sur HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).

Données supplémentaires pour la science des procédures pas à pas qui s’exécutent hello équipe données science des processus sont regroupés par hello **plateforme** qu’ils utilisent : 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Prédire les pourboires laissés aux taxis avec PySpark sur Azure Spark

Hello [Spark utilisation sur Azure HDInsight](machine-learning-data-science-spark-overview.md) procédure pas à pas utilise des données à partir de New York taxi toopredict si une info-bulle est payée et plage hello de quantités attendu toobe payé. Il utilise hello équipe données science des processus dans un scénario à l’aide un [cluster Azure HDInsight Spark](https://azure.microsoft.com/services/hdinsight/) toostore, Explorer, fonctionnalité ingénieur des données à partir de voyage taxi NYC disponible publiquement de hello et prix du jeu de données. Cette rubrique de présentation configure vous avec un cluster HDInsight Spark et le hello Jupyter PySpark blocs-notes utilisés dans le reste de hello de procédure pas à pas hello. Ces ordinateurs portables vous montrent comment tooexplore vos données et la procédure puis toocreate et utiliser des modèles. Hello avancé d’exploration de données et modélisation bloc-notes montre comment tooinclude la validation croisée, hyper-paramètre de balayage et évaluation du modèle.

### <a name="data-exploration-and-modeling-with-spark"></a>Exploration et modélisation des données avec Spark 
Explorer hello le jeu de données, de créer, d’évaluer et d’évaluer les modèles d’apprentissage automatique hello en passant par hello [créer des modèles de classification et de régression binaire pour les données avec les outils d’analyse hello Spark MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) rubrique.

### <a name="model-consumption"></a>Utilisation des modèles
toolearn comment créer des modèles de classification et la régression de hello tooscore dans cette rubrique, consultez [Score et évaluer les modèles d’apprentissage automatique de Spark intégrée](machine-learning-data-science-spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Validation croisée et balayage hyperparamétrique
consultez la page [Exploration et modélisation avancées des données avec Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) pour savoir comment entraîner les modèles à l’aide de la validation croisée et du balayage hyperparamétrique.


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Prédire les pourboires laissés aux taxis avec Scala sur Azure Spark

Hello [Scala utilisation avec Spark sur Azure](machine-learning-data-science-process-scala-walkthrough.md) procédure pas à pas utilise des données à partir de New York taxi toopredict si une info-bulle est payée et plage hello de quantités attendu toobe payé. Il montre comment toouse Scala pour les tâches d’apprentissage automatique supervisé avec la bibliothèque de formation ordinateur hello Spark (MLlib) et SparkML packages sur un cluster Azure HDInsight Spark. Il vous guide à travers les tâches hello constituant hello [processus de science des données](http://aka.ms/datascienceprocess): intégrer les données et exploration, de visualisation, l’ingénierie de fonctionnalité, modélisation et la consommation de modèle. les modèles de Hello générés incluent la régression logistique et linéaire, les forêts aléatoires et les arbres augmentés dégradés.


## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur les composants clés hello qui composent hello processus de science des données de Team, consultez [vue d’ensemble du processus de science des données équipe](data-science-process-overview.md).

Pour une présentation du cycle de vie de processus de science des données équipe hello que vous pouvez utiliser toostructure vos projets de science des données, consultez [cycle de vie des processus de science des données équipe](data-science-process-lifecycle.md). cycle de vie Hello décrit les étapes de hello, à partir du début toofinish, que les projets suivent généralement lorsqu’elles sont exécutées. 

