---
title: "aaaWhat est le processus de science des données équipe ?  | Microsoft Docs"
description: "Hello, processus de science des données équipe est une méthode systématique pour la création d’applications intelligentes qui tirent parti d’analytique avancée."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>Nouveautés hello processus de science des données équipe (TDSP)
Hello [processus de science des données équipe (TDSP)](data-science-process-overview.md) fournit une approche systématique toobuilding applications intelligentes qui permet aux équipes de données scientifiques toocollaborate efficacement hello du cycle de vie complet d’activités nécessaires tooturn ces applications dans les produits. Hello TDSP décrit une séquence d’étapes qui fournissent des **conseils** sur comment problème de hello toodefine, configurer les outils de hello et l’environnement nécessaire, analyser des données pertinentes, créer et évaluer les modèles prédictifs et ensuite déployer ces modèles dans applications d’entreprise. 

Voici les étapes de hello dans **processus de science des données équipe**:  

![Flux de travail CAP](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

processus de Hello est **itératif**: hello de nouveaux et existants ou des améliorations dans le modèle de hello évolue et nécessite retravailler les étapes précédemment effectuées dans l’ordre de hello. Développement d’organisation existante et les processus de planification de projet sont **facilement adaptables** toowork avec hello TDSP défini par la séquence d’étapes. 

Hello étapes dans le processus de hello sont représentées et liés Bonjour [cursus TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) et décrit ci-dessous.  

## <a name="preparation-steps"></a>Étapes de préparation
## <a name="p1-plan-hello-analytics-project"></a>P1. Planifier le projet hello analytique
Lancer un projet d’analyse en définissant des objectifs d’entreprise et une problématique. Ces éléments sont appelés **Exigences pour l'entreprise**. Un objectif central de cette étape est tooidentify hello commerciales clés variables (ventes de prévision ou hello probabilité d’une commande en cours frauduleuse, par exemple qui hello analyse besoins toopredict toosatisfy ces exigences). Une planification supplémentaire est alors généralement essentiel toodevelop comprendre hello **des sources de données** nécessaire tooaddress hello objectifs du projet hello du point de vue analytique. Il n’est pas rare, par exemple, toofind que les systèmes existants doivent toocollect et connecter d’autres types de données tooaddress hello problème et atteindre les objectifs de hello. Pour obtenir des instructions, consultez [planifier votre environnement pour hello processus de science des données équipe](machine-learning-data-science-plan-your-environment.md) et [scénarios d’analytique avancée dans Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Configurer un environnement d’analyse
Un environnement analytique pour hello processus de science des données équipe comprend plusieurs composants : 

* **espaces de travail données** où les données de salutation sont préparées pour une analyse et de modélisation, 
* un **infrastructure de traitement** pour le prétraitement, l’exploration et la modélisation des données de hello
* un **infrastructure du runtime** toooperationalize hello modèles analytiques et exécuter des applications client intelligent hello qui utilisent des modèles de hello.  

Hello analytique infrastructure dont a besoin le programme d’installation toobe est souvent partie d’un environnement qui est distinct à partir de systèmes opérationnels des noyaux. Mais en général, il s’appuie sur les données à partir de plusieurs systèmes au sein de l’entreprise de hello et entreprise toohello externe de sources. infrastructure d’analytique Hello peut être entièrement basée sur le cloud, ou une installation locale, ou un mélange de hello deux. Pour plus d’options, consultez [configurer des environnements de science des données pour une utilisation dans hello processus de science des données équipe](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Opérations d’analyse :
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Réception de données dans l’environnement d’analyse hello
première étape de Hello donnée toobring hello pertinentes à partir de diverses sources, soit à partir de dans ou à partir de l’entreprise en dehors de hello, dans une analyse des environnements où les données de salutation peuvent être traitées. Hello **format** Hello source de données peuvent différer de format hello requis par la destination de hello. Par conséquent, une transformation de données peut également avoir toobe effectué par les outils d’ingestion hello. Pour connaître les options, référez-vous à [Charger des données dans des environnements de stockage à des fins d'analyse](machine-learning-data-science-ingest-data.md)

Dans la réception initiale du toohello Ajout de données, de nombreuses applications intelligentes sont des données de hello toorefresh requis régulièrement dans le cadre d’un processus en cours de formation. Cette opération est possible grâce à la configuration d'un **pipeline de données** ou d'un flux de travail. Cela constitue une partie de la partie itératif de hello du processus hello qui inclut la reconstruction et réévaluer les modèles analytiques hello utilisés par l’application intelligente de hello déploiement hello solution. Voir, par exemple, [déplacer des données à partir d’un ordinateur local SQL server tooSQL Azure avec Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Explorer et pré-traiter des données
étape suivante de Hello est tooobtain une meilleure compréhension des données de salutation en étudiant ses **des statistiques de synthèse** , relations et à l’aide de techniques telles **visualisation**. C'est à ce niveau que les problèmes de **qualité des données** et d'intégrité, telles que les valeurs manquantes, les incompatibilités de type de données et les relations incohérentes entre les données sont gérés. Les transformations de pré-traitement sont utilisé tooclean des données brutes de hello avant analytique supplémentaire et modélisation peut avoir lieu. Pour obtenir une description, consultez [tooprepare des données pour l’apprentissage améliorée des tâches](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Développement de fonctionnalités
En collaboration avec des experts du domaine, les chercheurs de données doivent identifier les fonctionnalités de hello que les propriétés de marquants de hello capture du jeu de données hello et qui peuvent être mieux variables de clés de l’entreprise utilisé toopredict hello identifiées pendant la planification. Ces nouvelles fonctionnalités peuvent être dérivées de données existantes ou nécessitent toobe supplémentaires de données collectée. Ce processus est appelé **l’équipe d’ingénierie de fonctionnalité** et fait partie de hello décrit les principales étapes de la création d’un système efficace analytique prédictive. Cette étape nécessite une combinaison créative d’aperçus d’expertise et hello domaine obtenu à l’étape d’exploration de données hello. Pour obtenir des instructions, consultez [l’ingénierie dans hello processus de science des données équipe de fonctionnalité](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Créer des modèles prévisionnels
Les chercheurs de données créer des modèles analytiques principales variables toopredict hello identifiés par les exigences métier hello Bonjour étape à l’aide de données qui a été nettoyées et les fonctionnalités de planification. Systèmes d’apprentissage machine prend en charge plusieurs **algorithmes de modélisation** qui sont applicables tooa une grande variété de cas. Pour obtenir des instructions, consultez [comment toochoose des algorithmes pour l’équipe Azure Machine Learning](machine-learning-algorithm-choice.md).

Des chercheurs de données doivent choisir le modèle le plus approprié à leur tâche de prédiction hello et il n’est pas rare que les résultats à partir de plusieurs modèles doivent toobe combinée tooobtain hello obtenir de meilleurs résultats. Hello des données d’entrée pour la modélisation sont généralement réparties de façon aléatoire en trois parties :

* un jeu de données de formation 
* un jeu de données de validation 
* un jeu de données de test 

modèles de Hello sont générées à l’aide de hello **jeu de données d’apprentissage**. Hello combinaison optimale des modèles (avec des paramètres paramétrés) est sélectionné par l’exécution de modèles de hello et mesurer les erreurs de prédiction hello pour hello **jeu de données de validation**. Enfin hello **jeu de données de test** est tooevaluate utilisé hello des performances du modèle de hello choisi sur des données distinctes qui n’était pas utilisé tootrain ou valider le modèle de hello.  Pour les procédures, voir [comment tooevaluate modèle de performances dans Azure Machine Learning](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Déployer et utiliser des modèles
Une fois que nous disposons d’un ensemble de modèles qui fonctionnent bien, ils peuvent être **mis** pour les autres tooconsume d’applications. En fonction des besoins de l’entreprise hello, les prédictions sont faites dans **en temps réel** ou sur un **lot** base. toobe mis, hello offrent toobe exposé avec un **ouvrir l’interface API** facilement utilisable à partir de diverses applications ce site Web en ligne, des feuilles de calcul, tableaux de bord ou des applications d’entreprise et le serveur principal. Voir [Déploiement d'un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Résumé et étapes suivantes
Hello [processus de science des données équipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) est modelée comme une séquence d’étapes itérées qui **fournissent des conseils** sur des tâches hello nécessaire toouse avancé analytique toobuild des applications intelligentes. Chaque étape fournit également des informations sur comment toouse décrit diverses tâches de hello toocomplete technologies Microsoft. 

Alors que TDSP n’impose pas de types spécifiques de **documentation** artefacts, il s’agit d’une pratique toodocument hello optimale d’évaluation, la modélisation et exploration de données hello et toosave hello code pertinente afin que hello analysis itération peut effectuée à la demande. Cela permet également de réutiliser hello analytique fonctionne lorsque vous travaillez sur d’autres applications qui impliquent des données similaires et des tâches de prédiction.

Complète de bout en bout pour les procédures pas à pas qui illustrent le processus hello pour toutes les étapes de hello **des scénarios spécifiques** sont également fournis. Consultez, par exemple :

* [Hello processus de science des données équipe en action : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Hello processus de science des données équipe en action : à l’aide de clusters HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).
* [Science des données avec Spark sur Azure HD.mdnsight](machine-learning-data-science-spark-overview.md)
* [Science des données évolutive dans Azure Data Lake :  une procédure de bout en bout](machine-learning-data-science-process-data-lake-walkthrough.md)

