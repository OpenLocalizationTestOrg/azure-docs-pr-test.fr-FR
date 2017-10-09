---
title: "aaaAzure équipe données Science leur cycle de vie | Documents Microsoft"
description: "Étapes nécessaires tooexecute vos projets de science des données."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Cycle de vie du processus TDSP (Team Data Science Process)

Hello, processus de science des données équipe (TDSP) fournit un cycle de vie recommandée que vous pouvez utiliser toostructure vos projets de science des données. cycle de vie Hello décrit les étapes de hello, à partir du début toofinish, que les projets suivent généralement lorsqu’elles sont exécutées. Si vous utilisez un autre cycle de vie des données scientifiques, tel que [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) ou votre processus personnalisé de l’organisation, vous pouvez toujours utiliser hello basé sur des tâches TDSP avec ces cycles de vie de développement. 

Ce cycle de vie a été conçu pour les projets de science des données qui sont tooship prévue dans le cadre d’applications intelligentes. Ces applications déploient des modèles d’apprentissage automatique ou d’intelligence artificielle pour l’analytique prédictive. Les projets de sciences des données exploratoires et les projets d’analytique ad hoc peuvent également tirer parti de ce processus. Mais dans ces cas, certaines étapes décrites peuvent s’avérer superflues.    

Voici une représentation visuelle de hello **cycle de vie des processus de science des données équipe**. 

![Cycle de vie du processus TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

cycle de vie Hello TDSP se compose de cinq étapes majeures qui sont exécutées de manière itérative. Vous avez notamment vu les points suivants :

* **Présentation de l’entreprise**
* **Acquisition de données et compréhension**
* **Modélisation**
* **Déploiement**
* **Acceptation du client**

Pour chaque phase, nous fournissons hello informations suivantes :

* **Objectifs**: hello des objectifs spécifiques.
* **Comment toodo il**: hello décrits des tâches spécifiques et les instructions fournies sur les compléter.
* **Artefacts**: hello livrables et hello prennent en charge de production.


## <a name="1-business-understanding"></a>1. Présentation de l’entreprise

### <a name="goals"></a>Objectifs
* Hello **clé variables** sont spécifiés qui sont tooserve comme hello **modèle cibles** et dont les métriques connexes sont utilisés déterminer la réussite de hello pour le projet de hello.
* Hello pertinentes **des sources de données** sont identifiés qu’accès tooor besoins tooobtain business de hello.

### <a name="how-toodo-it"></a>Comment toodo il
Deux tâches principales sont traitées dans cette phase : 

* **Définir des objectifs**: travailler avec votre client et d’autres toounderstand les parties prenantes et identifier les problèmes métier hello. Formuler des questions qui définissent les objectifs de l’entreprise hello et que les techniques de science des données peuvent cibler.
* **Identifiez les sources de données**: rechercher hello applique les données qui vous permet de répondent aux questions de hello qui définissent des objectifs du projet de hello hello.

#### <a name="11-define-objectives"></a>1.1 Définir les objectifs

1. Un objectif de central de cette étape est la clé de hello tooidentify **variables d’activité** qu’analysis de hello doit toopredict. Ces variables sont visées tooas hello **modèle cibles** et métriques hello associées sont toodetermine utilisé hello cas de réussite du projet de hello. Deux exemples de ces cibles sont la probabilité de prévision ou hello ventes d’une commande de fraude.

2. Définir hello **objectifs du projet** en demandant et affiner les questions « sharp » qui sont pertinentes et spécifiques et non équivoque. Science des données consiste à hello à l’aide de noms et des chiffres tooanswer ces questions. Pour poser des questions AIGUES plus d’informations, consultez [comment toodo science des données](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blog. Recherche de données / machine learning n’est généralement utilisé tooanswer cinq types de questions :
 
   * Quelle quantité (ou combien) ? (régression)
   * Quelle catégorie ? (classification)
   * Quel groupe ? (clustering)
   * Est-ce étrange ? (détection des anomalies)
   * Quelle est l’option appropriée ? (recommandation)

    Déterminez laquelle de ces questions vous posez et comment le fait d’y répondre vous permet d’atteindre vos objectifs professionnels.

3. Définir hello **équipe de projet** en spécifiant des rôles de hello et les responsabilités de ses membres. Développez un plan à étapes général auquel vous vous référez au fil de la découverte de nouvelles informations.  

4. **Définissez des mesures de réussite**. Par exemple : obtenir de précision de prédiction de l’évolution du client de X % en fin de hello de ce projet de 3 mois, afin que nous pouvons proposer des promotions tooreduce évolution. Hello mesures doivent être **SMART**: 
   * **S**pécifiques 
   * **M**esurables
   * **A**tteignables 
   * **R**elevant (pertinentes) 
   * **T**ime-bound (associées à un délai) 

#### <a name="12-identify-data-sources"></a>1.2 Identifier les sources de données
Identifiez les sources de données qui contiennent des exemples connus de questions aigu tooyour de réponses. Recherchez hello données suivantes :

* Données **pertinents** toohello question. Nous avons de mesures cible de hello et des fonctionnalités qui sont associées toohello cible ?
* Les données qui sont un **mesure exacte** de nos fonctionnalités de modèle cible et hello dignes d’intérêt.

Il n’est pas rare, par exemple, toofind que les systèmes existants doivent toocollect et connecter d’autres types de données tooaddress hello problème et atteindre les objectifs de hello. Dans ce cas, vous pouvez souhaitez toolook pour les sources de données externes ou mettre à jour vos données de nouveaux systèmes toocollect.

### <a name="artifacts"></a>Artefacts
Voici les livrables hello dans cette étape :

* [**Affréter Document**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): un modèle standard est fourni dans hello définition TDSP de la structure de projet. Il s’agit d’un document actif qui est mis à jour tout au long du projet de hello nouvelles détections sont effectuées et en tant qu’entreprise besoins changent. clé de Hello est tooiterate sur ce document, en ajoutant plus de détails, au cours de processus de découverte hello. Conserver hello client et autres parties prenantes de hello de modifications et communiquent clairement les raisons hello hello modifications toothem.  
* [**Sources de données**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): il s’agit de hello **des Sources de données brutes** section Hello **des définitions de données** rapport qui se trouve dans le projet TDSP hello **rapport de données**  dossier. Il spécifie hello d’origine et les emplacements de destination pour les données brutes de hello. À un stade ultérieur, renseignez les détails supplémentaires tooyour scripts toomove hello données analytiques environnement.  
* [**Les dictionnaires de données**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): ce document fournit des descriptions de données hello qui sont fournies par hello client. Ces descriptions incluent des informations sur le schéma hello (types de données, des informations sur les règles de validation, le cas échéant) et hello diagrammes d’entité-relation si elle est disponible.


## <a name="2-data-acquisition-and-understanding"></a>2. Acquisition de données et compréhension

### <a name="goals"></a>Objectifs
* Nettoyage de qualité dataset dont relations toohello cible les variables sont compris qui se trouvent dans un environnement approprié analytique de hello, toomodel prêt.
* Une architecture de solution de toorefresh de pipeline de données hello et le score de données a été régulièrement développées.

### <a name="how-toodo-it"></a>Comment toodo il
Trois tâches principales sont traitées dans cette phase :

* **Réception des données de salutation** dans l’environnement analytique de hello cible.
* **Explorer les données hello** toodetermine si la qualité des données hello est question de hello tooanswer adéquates. 
* **Configurer un pipeline de données** tooscore à new ou régulièrement actualisé les données.

#### <a name="21-ingest-hello-data"></a>2.1 réception des données de salutation
Configurer hello processus toomove hello données à partir des emplacements sources toohello emplacements où les opérations d’analytique telles que la formation et les prédictions sont toobe exécutée. Pour obtenir des détails techniques et les options sur toodo avec divers services de données Azure, voir [charger des données dans des environnements de stockage pour l’analytique](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-hello-data"></a>2.2 Explorer les données de hello
Avant de vous entraîner à vos modèles, vous devez toodevelop bien les données de salutation. Les jeux de données réels sont souvent parasités, ne contiennent pas certaines valeurs ou comportent une multitude d’autres anomalies. Visualisation et synthèse des données peuvent être utilisé tooaudit hello la qualité de vos données et fournissent des informations de hello nécessaire tooprocess hello les données avant qu’il soit prêt pour la modélisation. Ce processus est souvent itératif.

TDSP fournit un utilitaire automatisé appelé [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp visualiser les données de hello et préparer les rapports de synthèse de données. Nous vous recommandons de commencer avec IDEAR première tooexplore hello données toohelp présentation initiale des données interactive avec aucun codage de développer et puis écrire du code personnalisé pour l’exploration de données et la visualisation. Pour obtenir des conseils sur le nettoyage des données de hello, consultez [tooprepare des données pour l’apprentissage améliorée des tâches](machine-learning-data-science-prepare-data.md).  

Une fois que vous êtes satisfait de la qualité de hello de données de salutation nettoyée, hello prochaine étape consiste toobetter comprendre les modèles hello inhérents aux données hello qui vous aident à choisissent et développement un modèle prédictif approprié pour votre cible. Rechercher les preuves pour correctement les données de salutation connecté sont toohello cible et s’il existe suffisamment toomove de données par progression avec des étapes de modélisation suivants hello. Là encore, ce processus est souvent itératif. Vous devrez peut-être toofind de nouvelles sources de données avec plus précis ou plus approprié données tooaugment hello jeu de données identifié dans l’étape précédente de hello.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 Configurer un pipeline de données
En outre les vitesses d’ingestion toohello initiale et le nettoyage des Bonjour des données, vous avez généralement besoin tooset un tooscore traiter les données nouvelles ou les actualiser les données hello régulièrement dans le cadre d’un processus en cours de formation. Cette opération est possible grâce à la configuration d’un pipeline de données ou d’un flux de travail. Voici une [exemple](machine-learning-data-science-move-sql-azure-adf.md) de façon tooset un pipeline avec [Azure Data Factory](https://azure.microsoft.com/services/data-factory/). 

Une architecture de solution du pipeline de données hello est développée dans cette étape. pipeline de Hello est également développé en parallèle avec hello suivant les étapes d’un projet de science des données hello. pipeline de Hello peut être basée sur le traitement par lots ou de diffusion en continu/en temps réel ou un hybride en fonction de votre entreprise a besoin et hello des contraintes de vos systèmes existants dans lequel cette solution est en cours d’intégration. 

### <a name="artifacts"></a>Artefacts
les Voici Hello hello livrables dans cette étape.

* [**Rapports de qualité des données**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): ce rapport contient des résumés de données, des relations entre chaque attribut et la cible, la variable de classement hello de etc. [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) outil fourni comme partie de TDSP peut rapidement générer Ce rapport sur n’importe quel jeu de données tabulaire comme un fichier CSV ou d’une table relationnelle. 
* **Architecture de solution**: cela peut être un diagramme ou la description du score de données pipeline utilisé toorun ou des prédictions sur les nouvelles données une fois que vous avez créé un modèle. Il contient également des tooretrain de pipeline hello votre modèle basé sur les nouvelles données. document de Hello est stocké dans hello [projet](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) lorsque vous utilisez le modèle de structure de répertoire TDSP hello.
* **La décision de point de contrôle**: avant de commencer, l’équipe d’ingénierie complète des fonctionnalités et de la construction d’un modèle, vous pouvez réévaluer hello projet toodetermine si la valeur hello attendue est suffisamment toocontinue poursuivi il. Par exemple, vous pouvez être prêt tooproceed, toocollect du besoin de davantage de données ou abandonner le projet de hello car les données de salutation n’existent pas de question de hello tooanswer.


## <a name="3-modeling"></a>3. Modélisation

### <a name="goals"></a>Objectifs
* Fonctionnalités de données optimal pour le modèle d’apprentissage automatique hello.
* Un modèle ML informatif qui prédit les cibles hello plus précisément.
* Modèle d’apprentissage automatique qui convient pour la production.

### <a name="how-toodo-it"></a>Comment toodo il
Trois tâches principales sont traitées dans cette phase :

* **L’équipe d’ingénierie de fonctionnalité**: créer des fonctionnalités de données à partir de l’apprentissage du modèle toofacilitate hello données brutes.
* **Modèle d’apprentissage**: trouver hello modèle question réponses hello plus précisément en comparant leurs critères de réussite.
* Déterminez si votre modèle est **approprié pour la production**.

#### <a name="31-feature-engineering"></a>3.1 Ingénierie des caractéristiques
Ingénierie de fonctionnalité implique la transformation de variables brutes toocreate, d’inclusion et agrégation hello fonctionnalités utilisées dans l’analyse de hello. Si vous souhaitez connaître les causes un modèle, vous devez toounderstand comment les fonctionnalités sont associée tooeach autres et comment les algorithmes d’apprentissage automatique hello sont toouse ces fonctionnalités. Cette étape nécessite une combinaison créative d’expertise du domaine et les informations obtenues à partir de l’étape d’exploration de données hello. Elle consiste à trouver un équilibre entre, d’une part, rechercher et inclure des variables informatives et, d’autre part, éviter un nombre trop élevé de variables non liées. Variables informatifs améliorent nos résultats ; variables non liées introduisent inutiles dans le modèle de hello. Vous devez également toogenerate ces fonctionnalités pour toutes les nouvelles données obtenues au cours du calcul de score. Par conséquent, génération hello de ces fonctionnalités peut dépendre uniquement des données qui sont disponibles au moment de hello de score. Pour obtenir des conseils techniques sur l’ingénierie de fonctionnalité lors de l’utilisation des différentes technologies de données Azure, consultez [l’ingénierie dans hello processus de science des données de fonctionnalité](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 Apprentissage du modèle
Selon le type de question auquel vous essayez de réponse, il existe de nombreux algorithmes de modélisation. Pour obtenir des conseils sur le choix des algorithmes de hello, consultez [comment toochoose des algorithmes pour Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md). Bien que cet article est écrit pour Azure Machine Learning, hello instructions qu’il contient est utile pour les projets d’apprentissage. 

processus Hello pour l’apprentissage du modèle inclut hello comme suit : 

* **Hello de fractionner les données d’entrée** aléatoire pour la modélisation dans un jeu de données d’apprentissage et un jeu de données de test.
* **Générer des modèles de hello** à l’aide du jeu de données d’apprentissage hello.
* **Évaluer** (jeu de données d’apprentissage et de test) une série de concurrents algorithmes d’apprentissage, ainsi que de hello différents paramétrage paramètres associés (connues en tant que paramètre de balayage) qui sont destinées à répondre à question hello d’intérêt avec hello données actuelles.
* **Déterminer la solution de « meilleure » hello** question de hello tooanswer en comparant les mesures de réussite hello entre d’autres méthodes.

> [!NOTE]
> **Éviter la fuite de**: toute fuite de données peut être dû par inclusion hello de données de dataset d’apprentissage hello externe qui permet à un modèle ou un algorithme d’apprentissage automatique des prédictions de bonne réaliste toomake. Fuite est une raison courante : pourquoi les chercheurs de données-nerveux quand des résultats PRÉDICTIFS qui semblent trop bonne toobe true. Ces dépendances peuvent être toodetect dur. tooavoid fuite requiert souvent une itération entre la création d’un jeu de données d’analyse, création d’un modèle et l’évaluation d’analyse de précision hello. 
> 
> 

Nous fournissons une [outil automatisée de modélisation et de création de rapports](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) TDSP qui est en mesure de toorun via plusieurs algorithmes et paramètre balaye tooproduce un modèle de ligne de base. Il génère également un rapport de modélisation de base qui résume les performances de chaque combinaison de modèle et de paramètre, y compris l’importance des variables. Ce processus est également itératif, car il peut influer sur l’ingénierie des caractéristiques. 

### <a name="artifacts"></a>Artefacts
les artefacts Hello produites dans cette étape sont les suivantes :

* [**Jeux de fonctionnalités**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): hello décrit les fonctions hello développées pour la modélisation de hello **ensembles de fonctionnalités** section Hello **définition de données** rapport. Il contient les fonctions hello toogenerate pointeurs toohello code et une description de la fonctionnalité de hello a été générée.
* [**Modèle de rapport**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): pour chaque modèle tenté, un rapport standard basé sur le modèle fournissant des détails sur chaque expérience est produit.
* **La décision de point de contrôle**: déterminer si le modèle de hello effectue également assez toodeploy il système de production tooa. Certains tooask questions clés sont les suivantes :
  * Question de hello réponses hello modèle avec une confiance suffisante compte tenu des données de test hello ? 
  * Est-il nécessaire d’essayer d’autres approches : collecter des données supplémentaires, poursuivre l’ingénierie des caractéristiques ou faire des essais avec d’autres algorithmes ?


## <a name="4-deployment"></a>4. Déploiement

### <a name="goal"></a>Objectif
* Les modèles avec un pipeline de données sont déployées tooa environnement de production ou de type production pour l’acceptation de l’utilisateur final. 

### <a name="how-toodo-it"></a>Comment toodo il
tâche principale Hello traité dans cette étape :

* **Mettre le modèle de hello**: déployer hello modèle et le pipeline tooa environnement de production ou de type production pour la consommation de l’application.

#### <a name="41-operationalize-a-model"></a>4.1 Faire fonctionner un modèle
Une fois que vous avez un ensemble de modèles qui fonctionnent bien, ils peuvent être operationalized pour les autres tooconsume d’applications. En fonction des besoins de l’entreprise hello, les prédictions sont faites en temps réel ou sur une base de lot. toobe mis, les modèles de hello ont toobe exposé avec une interface API ouvrir facilement utilisable à partir de différentes applications telles que les sites Web en ligne, des feuilles de calcul, des tableaux de bord ou des applications d’entreprise et le serveur principal. Pour obtenir des exemples de mise en œuvre de modèle avec un service web Azure Machine Learning, consultez [Déploiement d’un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md). Il est également une télémétrie toobuild de meilleure pratique et surveillance à hello du modèle de production et hello toohelp pipeline déployé de données avec l’état système ultérieures reporting et le dépannage.  

### <a name="artifacts"></a>Artefacts
* Tableau de bord d’état de mesures clés et d’intégrité du système.
* Rapport de modélisation final avec les détails du déploiement.
* Document final de l’architecture de la solution.

## <a name="5-customer-acceptance"></a>5. Acceptation du client

### <a name="goal"></a>Objectif
* **Finaliser les livrables hello**: Vérifiez que le pipeline de hello, modèle de hello et leur déploiement dans un environnement de production sont conformes aux objectifs du client.

### <a name="how-toodo-it"></a>Comment toodo il
Deux tâches principales sont traitées dans cette phase :

* **Validation du système**: confirmer le modèle de hello déployé et le pipeline sont répond bien aux besoins des clients.
* **Transfert de projet**: entité toohello toorun hello système de production.

client de Hello doit valider que système de hello répond à leurs besoins et les réponses hello hello questions avec précision toodeploy hello système tooproduction pour une utilisation par leur application cliente. Toute la documentation hello est et la finalisation. Un transfert de l’entité de toohello du projet hello responsable des opérations est terminée. Cette entité peut être, par exemple, un service informatique ou équipe de science des données client ou un agent du client de hello est chargé d’exécuter le système de hello en production. 

### <a name="artifacts"></a>Artefacts
artefact de principal Hello produite dans cette étape finale est hello **sortie de projet de rapport client**. Ce rapport technique de hello contenant tous les détails du projet de hello que toolearn utile sur et applique hello système. Un modèle de [Rapport de clôture](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) est fourni par le processus TDSP, qui peut être utilisé en l’état ou personnalisé en fonction des besoins du client. 

## <a name="summary"></a>Résumé
Hello [cycle de vie des processus de science des données équipe](http://aka.ms/datascienceprocess) est modelée comme une séquence d’étapes itérées qui fournissent des conseils sur les tâches hello nécessaire toouse des modèles prédictifs. Ces modèles peuvent être déployés dans un environnement production toobe exploitée toobuild intelligent applications. Hello ce cycle de vie des processus vise toocontinue toomove un projet de science des données vers l’avant vers un point de terminaison engagement clair. S’il est vrai que la science des données sont un exercice de la recherche et la découverte, en cours tooclearly en mesure de communiquer ces équipe tooyour de tâches et de vos clients à l’aide d’un ensemble bien défini d’artefacts que les modèles standard employés peuvent aider à éviter malentendu et augmenter les chances de hello d’un état de réussite d’un projet de science des données complexes.

## <a name="next-steps"></a>Étapes suivantes
Complète de bout en bout pour les procédures pas à pas qui illustrent le processus hello pour toutes les étapes de hello **des scénarios spécifiques** sont également fournis. Ils sont répertoriés et liées avec les descriptions de miniatures Bonjour [procédures pas à pas du processus de science des données équipe](data-science-process-walkthroughs.md) rubrique.

