---
title: "scénarios d’aaaIdentify et planifier votre processus analytique - Azure | Documents Microsoft"
description: "Planifiez une analyse avancée en imaginant une série de questions clés."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Comment tooidentify scénarios et plan pour advanced analytique le traitement des données
Quelles ressources vous prévoyez tooinclude lors de la configuration d’un environnement toodo avancée analytique de traitement sur un jeu de données ? Cet article propose une série de questions tooask qui permettra d’identifier les tâches de hello et les ressources appropriées à votre scénario. ordre de Hello des principales étapes à suivre pour l’analytique prédictive est décrit dans [What ' s hello processus de science des données équipe (TDSP) ?](data-science-process-overview.md). Chacune de ces étapes requiert des ressources spécifiques pour le scénario particulier de hello tâches tooyour pertinentes. Bonjour questions clés tooidentify votre scénario préoccupation données logistiques, caractéristiques, hello de qualité de jeux de données hello et les outils hello et langues que vous préférez analyse de hello toodo.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>Questions logistiques : emplacements et déplacement des données
les questions logistique Hello concernent emplacement hello Hello **source de données**, hello **destination cible** dans Azure et configuration requise pour le déplacement des données hello, y compris la planification de hello et des ressources impliqués. les données de salutation peut-être toobe déplacé plusieurs fois au cours du processus d’analytique hello. Un scénario courant consiste à toomove des données locales dans une forme de stockage sur Azure, puis dans Machine Learning Studio.

1. **Quelle est votre source de données ?** Est-il local ou dans le cloud de hello ? Par exemple :
   
   * les données de salutation sont publiquement disponibles à une adresse HTTP.
   * les données de salutation se trouvent dans un emplacement de fichier/réseau local.
   * les données de salutation sont dans une base de données SQL Server.
   * les données de salutation sont stockées dans un conteneur de stockage Azure
2. **Qu’est hello destination Azure ?** Où faut-il toobe pour le traitement ou la modélisation ? Par exemple :
   
   * un stockage Azure Blob
   * Bases de données SQL Azure
   * SQL Server dans les machines virtuelles Azure
   * HDInsight (Hadoop sur Azure) ou tables Hive
   * Azure Machine Learning
   * Disques durs virtuels Azure montables.
3. **Comment allez-vous les données de salutation toomove ?**  hello procédures et les ressources disponibles tooingest ou charger des données dans un large éventail d’environnements de traitement et de stockage différents sont décrites dans les rubriques suivantes de hello.
   
   * [Charger des données dans des environnements de stockage à des fins d’analyse](machine-learning-data-science-ingest-data.md)
   * [Importation de vos données d’apprentissage Azure Machine Learning Studio depuis différentes sources de données](machine-learning-data-science-import-data.md)
4. **Les données de salutation doit-elle toobe déplacé selon une planification régulière ou modifiés pendant la migration ?** Envisagez d’utiliser la fabrique de données Azure (ADF) lorsque les données besoins toobe migrés en permanence, en particulier si un scénario hybride qui accède à la fois localement et ressources de cloud est impliqué, ou lorsque hello données sont traitées ou doit toobe modifié ont une logique métier ajouté tooit cours hello en cours de migration. Pour plus d’informations, consultez [déplacer des données à partir d’un ordinateur local SQL server tooSQL Azure avec Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)
5. **La quantité de données de hello est toobe déplacé tooAzure ?** Les jeux de données très volumineux peuvent dépasser la capacité de stockage hello de certains environnements. Pour obtenir un exemple, consultez la discussion hello des limites de taille de Machine Learning Studio, dans la section suivante de hello. Dans ce cas, un échantillon de données de hello peut-être être utilisé pendant l’analyse de hello. Pour savoir comment toodown-exemple un jeu de données dans différents environnements Azure, consultez [les exemples de données Bonjour processus de science des données équipe](machine-learning-data-science-sample-data.md).

## <a name="data-characteristics-questions-type-format-and-size"></a>Questions sur les caractéristiques des données : type, format et taille
Ces questions est tooplanning clé votre stockage et de traitement des environnements, chacun d'entre eux sont toovarious approprié types de données et chacune d’elles comportent certaines restrictions.

1. **Quels sont les types de données hello ?** Par exemple :
   
   * Numérique
   * Par catégorie
   * Chaînes
   * Fichier binaire
2. **Quel est le format de vos données ?** Par exemple :
   
   * Fichiers plats séparés par des virgules (CSV) ou séparées par une tabulation (TSV)
   * Compressés ou non
   * Objets blob Azure
   * Tables Hadoop Hive
   * Tables SQL Server
3. **Quel volume vos données représentent-elles ?**
   
   * Petit : moins de 2 Go
   * Moyen : entre 2 Go et 10 Go
   * Grand : supérieur à 10 Go

Prenons l’exemple environnement d’Azure Machine Learning Studio hello :

* Pour obtenir la liste des formats de données hello et des types pris en charge par Azure Machine Learning Studio, consultez [des formats de données et les types de données pris en charge](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) section.
* Pour plus d’informations sur les limitations de données pour Azure Machine Learning Studio, consultez hello **comment grand jeu de données hello possible pour mon modules ?** section [importation et exportation de données pour l’apprentissage](machine-learning-faq.md#machine-learning-studio-questions)

Pour plus d’informations sur les limitations de hello d’autres services Azure utilisés dans le processus d’analytique hello, consultez [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md).

## <a name="data-quality-questions-exploration-and-pre-processing"></a>Questions sur la qualité des données : exploration et prétraitement
1. **Que savez-vous sur vos données ?** Explorer les données lorsque vous avez besoin d’une présentation de toogain ses caractéristiques. Par exemple les modèles ou les tendances qu’elles dévoilent, les aberrations qu’elles contiennent ou le nombre de valeurs manquantes. Cette étape est importante pour déterminer l’étendue de hello de pré-traitement si nécessaire, pour formuler des hypothèses qui pourrait suggérer des fonctionnalités les plus appropriées hello ou type d’analyse, de la formulation de plans de collecte de données supplémentaires. Le calcul des statistiques descriptives et le tracé des visualisations sont des techniques utiles pour l’inspection des données. Pour plus d’informations de tooexplore un jeu de données dans différents environnements Azure, voir [Explorer les données Bonjour processus de science des données équipe](machine-learning-data-science-explore-data.md).
2. **Les données de salutation nécessite-t-il de pré-traitement ou de nettoyage ?**
   Le prétraitement et le nettoyage des données sont des tâches importantes qui doivent intervenir avant d'utiliser un jeu de données à des fins d'apprentissage automatique. Les données brutes sont souvent bruyantes, peu fiables et incomplètes. Leur utilisation pour la modélisation peut générer des résultats trompeurs. Pour obtenir une description, consultez [tooprepare des données pour l’apprentissage améliorée des tâches](machine-learning-data-science-prepare-data.md).

## <a name="tools-and-languages-questions"></a>Questions sur les outils et les langues
Il existe un grand nombre de possibilités en fonction des langues, des environnements de développement et des outils dont vous avez besoin ou avec lesquels vous êtes le plus à l’aise.

1. **Langues comment vous préférez toouse pour l’analyse ?**  
   
   * R
   * Python
   * SQL
2. **Quels outils devez-vous utiliser pour l’analyse des données ?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -un langage de script utilisé tooadminister vos ressources Azure dans un langage de script.
   * [Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)
   * [Revolution Analytics](http://www.revolutionanalytics.com/revolution-r-open)
   * [RStudio](http://www.rstudio.com)
   * [Python Tools pour Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Blocs-notes Jupyter](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>Identification de votre scénario d’analyse avancée
Une fois que vous avez répondu aux questions hello dans la section précédente de hello, vous êtes prêt toodetermine celui qui correspond à votre cas. exemples de scénarios de Hello sont décrites dans [scénarios d’analytique avancée dans Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).

