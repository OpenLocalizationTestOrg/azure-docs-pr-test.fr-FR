---
title: "aaaDemand prévision dans le Guide technique de l’énergie | Documents Microsoft"
description: "Un guide technique toohello modèle de Solution avec Business Intelligence de Microsoft Cortana pour la prévision de l’énergie de la demande."
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>Guide technique toohello Cortana Intelligence Solution de modèle de prévision de l’énergie de la demande
## <a name="overview"></a>**Vue d'ensemble**
Modèles de solution sont conçues tooaccelerate hello consistant à générer une démonstration E2E par-dessus Cortana Intelligence Suite. Un modèle déployé provisionner votre abonnement avec le composant Cortana Intelligence nécessaire et établir des relations entre hello. Il alimente également pipeline de données hello avec des exemples de données générés à partir d’une application de simulation des données. Télécharger le simulateur de données hello à partir du lien hello fourni et l’installer sur votre ordinateur local, consultez le fichier Lisezmoi.txt de toohello pour obtenir des instructions sur l’utilisation de simulateur de hello. Données générées à partir du simulateur de hello seront hydrate pipeline de données hello et commencer à générer la prédiction d’apprentissage machine qui peut ensuite être visualisée dans le tableau de bord Power BI hello.

modèle de solution Hello [ici](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

processus de déploiement Hello va vous guider tout au long de plusieurs étapes tooset, vos informations d’identification de la solution. Assurez-vous que vous enregistrez ces informations d’identification telles que le nom de la solution, nom d’utilisateur et mot de passe indiqués au cours du déploiement de hello.

objectif Hello de ce document est l’architecture de référence tooexplain hello et différents composants configurés dans votre abonnement dans le cadre de ce modèle de Solution. document de Hello parle également comment tooreplace hello des exemples de données, avec des données réelles de votre propre toobe toosee en mesure d’insights/prédictions vous a gagné des données. En outre, hello document aborde les parties hello Hello modèle de Solution qui doivent toobe modifiée si vous souhaitez que les solutions de hello toocustomize avec vos propres données. Obtenir des instructions sur la façon dont toobuild hello du tableau de bord Power BI pour ce modèle de Solution sont fournies à la fin de hello.

## <a name="big-picture"></a>**Grandes lignes**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Architecture
Lors de la solution de hello est déployée, les divers services Azure dans Cortana Analytique Suite sont activés (*par exemple,* Event Hub, Stream Analytics, HDInsight, Data Factory, Machine Learning, *etc.*). diagramme d’architecture Hello ci-dessus montre, à un niveau élevé, comment hello prévision de la demande pour le modèle de Solution de l’énergie est construit à partir de bout en bout. Vous serez en mesure de tooinvestigate ces services en cliquant dessus sur hello diagramme de modèle de solution créé avec le déploiement hello de solution de hello. Hello les sections suivantes décrire chaque élément.

## <a name="data-source-and-ingestion"></a>**Source et ingestion de données**
### <a name="synthetic-data-source"></a>Source de données de synthèse
Pour ces données de hello du modèle source utilisé est généré à partir d’une application de bureau que vous allez télécharger et exécuter localement après un déploiement réussi. Vous recherchez toodownload d’instructions hello et installer cette application dans la barre des propriétés hello lorsque vous sélectionnez hello premier nœud appelé simulateur de données de prévision d’énergie sur le diagramme de modèle de solution hello. Cette application de flux de hello [concentrateur d’événements Azure](#azure-event-hub) service avec des points de données ou des événements, qui seront utilisés dans le reste de hello du flux de solution hello.

application de la génération des événements Hello remplira hello concentrateur d’événements Azure uniquement lors de son exécution sur votre ordinateur.

### <a name="azure-event-hub"></a>Azure Event Hub
Hello [concentrateur d’événements Azure](https://azure.microsoft.com/services/event-hubs/) service est destinataire hello d’entrée hello fournie par hello synthétique Source de données décrit ci-dessus.

## <a name="data-preparation-and-analysis"></a>**Préparation et analyse des données**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) service est utilisé tooprovide près analytique en temps réel sur les flux d’entrée de hello de hello [concentrateur d’événements Azure](#azure-event-hub) de service et de publier les résultats sur un [Power BI](https://powerbi.microsoft.com) tableau de bord, ainsi que l’archivage de tous les bruts toohello événements entrants [Azure Storage](https://azure.microsoft.com/services/storage/) service pour un traitement ultérieur par hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service.

### <a name="hd-insights-custom-aggregation"></a>Agrégation personnalisée HDInsight
Hello service de Azure HD Insight est utilisé toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) agrégations tooprovide de scripts (orchestrés par Azure Data Factory) sur des événements bruts hello qui ont été archivés à l’aide du service d’Analytique de flux de données Azure hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) service est utilisé (orchestrés par Azure Data Factory) toomake prévoir la consommation d’énergie de futures d’une région donnée, fonction d’entrées hello reçues.

## <a name="data-publishing"></a>**Publication des données**
### <a name="azure-sql-database-service"></a>Service de base de données SQL Azure
Hello [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/) service est reçues par hello service Azure Machine Learning qui est consommée Bonjour des prédictions de hello toostore utilisé (géré par Azure Data Factory) [Power BI](https://powerbi.microsoft.com) tableau de bord.

## <a name="data-consumption"></a>**Consommation des données**
### <a name="power-bi"></a>Power BI
Hello [Power BI](https://powerbi.microsoft.com) service est tooshow utilisé un tableau de bord contient des agrégations fournies par hello [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) service, ainsi que la demande des prévisions, stocké dans [SQL Azure Base de données](https://azure.microsoft.com/services/sql-database/) qui ont été générés à l’aide de hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) service. Pour obtenir des Instructions sur la façon dont toobuild hello du tableau de bord Power BI pour ce modèle de Solution, consultez la section toohello ci-dessous.

## <a name="how-toobring-in-your-own-data"></a>**Comment toobring vos données**
Cette section décrit comment toobring tooAzure de vos propres données et zones nécessiterait change pour les données de salutation vous amener à cette architecture.

Il est peu probable que vous mettez tout jeu de données correspondrait à hello le jeu de données utilisé pour ce modèle de solution. Présentation de vos données et la configuration requise sera essentiel dans la façon dont vous modifier toowork de ce modèle avec vos propres données. S’il s’agit de votre première toohello d’exposition service Azure Machine Learning, vous pouvez obtenir un tooit introduction à l’aide d’exemple hello dans [comment toocreate votre première expérience](machine-learning/machine-learning-create-experiment.md).

traite des sections hello du modèle hello qui requièrent des modifications lorsqu’un nouveau jeu de données est introduit Hello les sections suivantes.

### <a name="azure-event-hub"></a>Azure Event Hub
Hello [concentrateur d’événements Azure](https://azure.microsoft.com/services/event-hubs/) service est très générique, telles que les données peuvent être publiées toohello hub au format CSV ou JSON. Aucun traitement spécial ne se Bonjour concentrateur d’événements Azure, mais il est important de que vous familiariser avec les données hello qui sont chargées dans celui-ci.

Ce document ne décrit pas comment tooingest vos données, mais l’un peut facilement envoyer des événements ou des données tooan concentrateur d’événements Azure, à l’aide de hello [API de concentrateur d’événements](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) service est utilisé tooprovide près analytique en temps réel par la lecture à partir de flux de données et la sortie des données tooany de diverses sources.

Pourquoi la demande de prévision de modèle de Solution de l’énergie, hello Analytique de flux de données Azure constituée de deux sous-requêtes, chaque consomment des événements du service de concentrateur d’événements Azure de hello en tant qu’entrées et ayant des sorties tootwo des emplacements distincts. Ces sorties comprennent un jeu de données Power BI et un emplacement Azure Storage.

Hello [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) accessibles de requête :

* Connectez hello [portail de gestion Azure](https://manage.windowsazure.com/)
* Localisation des travaux hello stream analytique ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) qui ont été générés lors du déploiement de solutions de hello. Une est pour pousser le stockage des données tooblob (par exemple, mytest1streaming432822asablob) et hello autres une est pour pousser des données tooPower BI (par exemple, mytest1streaming432822asapbi).
* Sélectionnez

  * ***ENTRÉES*** entrée de requête hello tooview
  * ***REQUÊTE*** tooview hello requête
  * ***SORTIES*** tooview hello différentes sorties

Vous trouverez plus d’informations sur la construction de la requête Analytique de flux de données Azure Bonjour [référence de flux de requête Analytique](https://msdn.microsoft.com/library/azure/dn834998.aspx) sur MSDN.

Dans cette solution, hello tâche Analytique de flux de données Azure qui génère le dataset avec des informations d’analytique en temps réel sur hello entrant données flux tooa tableau de bord presque est fourni dans le cadre de ce modèle de solution. Étant donné qu’une connaissance implicite sur le format de données entrants hello, ces requêtes devez toobe modifiée en fonction de votre format de données.

Hello autre tâche Analytique de flux de données Azure génère tous les [concentrateur d’événements](https://azure.microsoft.com/services/event-hubs/) événements [Azure Storage](https://azure.microsoft.com/services/storage/) et ne nécessite donc aucune modification, quelle que soit votre format de données comme informations d’événement complet hello sont transmis en continu toostorage.

### <a name="azure-data-factory"></a>Azure Data Factory
Hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service orchestre le déplacement des hello et le traitement des données. Bonjour à la demande de prévision pour les données de modèle de Solution énergie hello fabrique est constituée de douze [pipelines](data-factory/data-factory-create-pipelines.md) qui déplacer et traiter les données hello à l’aide de différentes technologies.

  Vous pouvez accéder à votre fabrique de données en ouvrant le nœud de fabrique de données hello bas hello du diagramme de modèle de solution hello créé avec le déploiement hello de solution de hello. Cette opération prendra vous toohello fabrique de données sur le portail de gestion Azure. Si vous constatez des erreurs dans vos jeux de données, vous pouvez ignorer ceux qu’ils sont en raison de la fabrique de toodata en cours de déploiement avant le démarrage de générateur de données hello. Ces erreurs ne perturbent pas le fonctionnement de votre fabrique de données.

Cette section traite des hello nécessaire [pipelines](data-factory/data-factory-create-pipelines.md) et [activités](data-factory/data-factory-create-pipelines.md) contenus dans hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Voici la vue de diagramme hello de solution de hello.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Cinq de pipelines hello de cette fabrique contiennent [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts toopartition utilisée et les données d’agrégation hello. Lorsque cela est indiqué, les scripts hello se trouve dans hello [Azure Storage](https://azure.microsoft.com/services/storage/) compte créé pendant l’installation. à l’emplacement suivant : demandforecasting\\\\script\\\\hive\\\\ (ou https://[nom de votre solution].blob.core.windows.net/demandforecasting).

Toohello similaire [Analytique de flux de données Azure](#azure-stream-analytics-1) requêtes, le [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts ont une connaissance implicite sur le format de données entrants hello, ces requêtes devez toobe modifiée en fonction de votre format de date et [l’équipe d’ingénierie de fonctionnalité](machine-learning/machine-learning-feature-selection-and-engineering.md) configuration requise.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
Cela [pipeline](data-factory/data-factory-create-pipelines.md) pipeline contient une activité unique - une [HDInsightHive](data-factory/data-factory-hive-activity.md) à l’aide de l’activité un [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) qui exécute un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)en continu dans des données de la demande au niveau de la région de toohourly niveau sous-centrale hello tooaggregate de script toutes les 10 secondes et le placer dans [Azure Storage](https://azure.microsoft.com/services/storage/) tâche d’Analytique de flux de données Azure hello.

Le script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) utilisé pour cette tâche de partitionnement est ***AggregateDemandRegion1Hr.hql***

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
Ce [pipeline](data-factory/data-factory-create-pipelines.md) contient deux activités :

* [HDInsightHive](data-factory/data-factory-hive-activity.md) à l’aide de l’activité une [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que s’exécute une ruche tooaggregate hello toutes les heures l’historique des données à la demande au niveau de la région sous-centrale toohourly au niveau de script et la placer dans le stockage Azure pendant hello Azure Tâche de flux de données Analytique
* [Copie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activité qui déplace hello des données agrégées à partir de l’objet blob de stockage Azure toohello base de données SQL Azure qui a été configuré dans le cadre de l’installation du modèle de solution hello.

Hello [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) de script pour cette tâche est ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Ces [pipelines](data-factory/data-factory-create-pipelines.md) contient plusieurs activités et dont le résultat final est hello noté des prédictions à partir de l’expérience d’Azure Machine Learning hello associé à ce modèle de solution. Ils sont presque identiques, sauf chacun d’eux gère uniquement les hello autre région qui est effectuée par un autre RegionID passé au pipeline ADF hello et le script hive de hello pour chaque région.  
les activités Hello contenues dans ce sont :

* [HDInsightHive](data-factory/data-factory-hive-activity.md) à l’aide de l’activité une [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) qui exécute une ruche script tooperform agrégations, qu’il fonctionnalité nécessaire pour hello expérience Azure Machine Learning l’ingénierie. Hello scripts Hive pour cette tâche sont respectifs ***PrepareMLInputRegionX.hql***.
* [Copie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activité qui déplace les résultats hello hello [HDInsightHive](data-factory/data-factory-hive-activity.md) activité tooa unique objet blob Azure Storage qui est accessibles par hello [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) activité.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) activité qui appelle l’expérience d’Azure Machine Learning hello qui se traduit par hello entraîne être placé dans un seul objet blob de stockage Azure.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Ces [pipelines](data-factory/data-factory-create-pipelines.md) contienne une seule activité - un [copie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activité qui déplace les résultats hello Hello expérience Azure Machine Learning hello respectif ***MLScoringRegionXPipeline *** toohello base de données SQL Azure qui a été configuré dans le cadre de l’installation du modèle de solution hello.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
Cela [pipelines](data-factory/data-factory-create-pipelines.md) contienne une seule activité - un [copie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activité qui déplace hello agrégée des données à la demande en cours à partir de ***LoadHistoryDemandDataPipeline*** toohello Azure Base de données SQL a été configuré dans le cadre de l’installation du modèle de solution hello.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
Ces [pipelines](data-factory/data-factory-create-pipelines.md) contienne une seule activité - un [copie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activité qui déplace les données de référence hello de région/sous-centrale/Topologygeo qui sont téléchargés tooAzure objet blob de stockage dans le cadre de la solution de hello modèle toohello d’installation base de données SQL Azure qui a été configuré dans le cadre de l’installation du modèle de solution hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) faire des essais utilisés pour ce modèle de solution fournit prédiction hello de la demande de région. expérience de Hello est le jeu de données spécifique toohello consommée et nécessite donc des données spécifiques toohello modification ou de remplacement qui s’affiche dans.

## <a name="monitor-progress"></a>**Surveiller la progression**
Une fois que hello Générateur de données est lancé, pipeline hello commence tooget intégré et hello différents composants de votre solution démarrent son en action commandes hello émis par hello Data Factory. Il existe deux façons, que vous pouvez surveiller le pipeline de hello.

1. Vérifier les données de hello à partir du stockage d’objets Blob Azure.

    Un des travaux de flux de données Analytique hello écrit hello entrants données tooblob un stockage brut. Si vous cliquez sur **stockage d’objets Blob Azure** composant de votre solution hello écran vous solution de hello correctement déployé, puis cliquez sur **ouvrir** dans le volet droit de hello, il vous faudra toohello [Portail de gestion azure](https://portal.azure.com). Une fois dans le portail, cliquez sur **Objets BLOB**. Dans le panneau de configuration suivant hello, vous verrez une liste de conteneurs. Cliquez sur **energysadata**. Dans le panneau de configuration suivant hello, vous verrez hello **« demandongoing »** dossier. À l’intérieur du dossier de rawdata hello, vous verrez des dossiers avec des noms comme date = 2016-01-28 etc.. Si vous voyez ces dossiers, il indique que les données brutes hello sont correctement générée sur votre ordinateur et stockées dans le stockage d’objets blob. Vous devriez voir des fichiers avec des tailles finies en Mo dans ces dossiers.
2. Vérifiez les données de salutation à partir de la base de données SQL Azure.

    Hello dernière étape du pipeline de hello donnée toowrite (par exemple, les prédictions à partir de l’apprentissage) dans la base de données SQL. Vous pouvez avoir toowait un maximum de 2 heures pour hello données tooappear dans base de données SQL. Une façon toomonitor la quantité de données est disponible dans votre base de données SQL s’effectue via [portail de gestion Azure](https://manage.windowsazure.com/). Sur le panneau gauche hello localiser les bases de données SQL![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) et cliquez dessus. Recherchez ensuite votre base de données (par exemple, demo123456db), puis cliquez dessus. Sur la page suivante de hello sous **« Connexion base de données tooyour »** , cliquez sur **« Requêtes Transact-SQL d’exécution sur votre base de données SQL »**.

    Ici, vous pouvez cliquer sur Nouvelle requête et de requête pour le nombre de hello de lignes (par exemple, « select count à partir de DemandRealHourly) » à mesure que votre base de données augmente, hello nombre de lignes dans la table de hello doit augmenter.)
3. Vérifier les données de hello à partir du tableau de bord Power BI.

    Vous pouvez configurer Power BI chemin réactif du tableau de bord toomonitor hello entrantes données brutes. Veuillez suivre les instructions hello Bonjour section « Tableau de bord Power BI ».

## <a name="power-bi-dashboard"></a>**Tableau de bord Power BI**
### <a name="overview"></a>Vue d'ensemble
Cette section décrit comment tooset des toovisualize du tableau de bord Power BI vos données en temps réel à partir d’Azure stream analytique (chemin d’accès à chaud), en tant que résultats ainsi que les prévisions à partir de Azure d’apprentissage (chemin d’accès à froid).

### <a name="setup-hot-path-dashboard"></a>Configurer le tableau de bord de chemin à chaud
vous guide Hello suit comment toovisualize en temps réel de sortie de données à partir de l’Analytique des flux de travaux qui ont été générées au moment de hello du déploiement de la solution. A [Power BI en ligne](http://www.powerbi.com/) compte est hello tooperform requis comme suit. Si vous ne possédez pas de compte, vous pouvez en [créer un](https://powerbi.microsoft.com/pricing).

1. Ajouter une sortie Power BI dans Azure Stream Analytics (ASA).

   * Vous devez obtenir des instructions de hello toofollow dans [Analytique de flux de données Azure et Power BI : un tableau de bord analytique en temps réel pour la visibilité en temps réel des flux de données](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset de sortie hello de votre travail Analytique des flux de données Azure en tant que votre puissance Tableau de bord BI.
   * Recherchez la tâche analytique hello stream dans votre [portail de gestion Azure](https://manage.windowsazure.com). nom Hello du travail de hello doit être : Nom_solution + streamingjob » » + nombre aléatoire + « asapbi » (c'est-à-dire demostreamingjob123456asapbi).
   * Ajouter une sortie de Power BI pour le travail ASA hello. Ensemble hello **Alias de sortie** en tant que **'PBIoutput'**. Dans **Nom du jeu de données** et **Nom de la table**, entrez **EnergyStreamData**. Une fois que vous avez ajouté une sortie de hello, cliquez sur **« Démarrer »** bas hello de tâche de flux de données Analytique hello page toostart hello. Un message de confirmation doit s’afficher (*par exemple*: La tâche Stream Analytics ’myteststreamingjob12345asablob’ a bien démarré).
2. Connectez-vous trop[Power BI en ligne](http://www.powerbi.com)

   * Sur hello gauche Panneau de configuration des groupes de données dans mon espace de travail, vous devez être en mesure de toosee un nouveau présentant de jeu de données sur le panneau gauche de hello de Power BI. Il s’agit de hello de diffusion en continu de données que vous envoyées à l’étape précédente de hello Analytique de flux de données Azure.
   * Vérifiez que hello ***visualisations*** volet est ouvert et qu’il est affiché sur le côté droit de l’écran hello.
3. Créer hello « À la demande par horodatage » vignette :

   * Cliquez sur le dataset **'EnergyStreamData'** sur hello section des jeux de données du Panneau de gauche.
   * Cliquez sur l’icône **Courbes** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * Cliquez sur EnergyStreamData dans le panneau **Champs** .
   * Cliquez sur **Horodatage** et vérifiez qu’il apparaît sous Axe. Cliquez sur **Charger** et vérifiez qu’il apparaît sous Valeurs.
   * Cliquez sur **enregistrer** hello haut et nommez le rapport hello en tant que « EnergyStreamDataReport ». rapport Hello nommé « EnergyStreamDataReport » s’affichera dans la section rapports dans le volet de navigation hello sur la gauche.
   * Cliquez sur **« Pin visuelles »** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) icône dans le coin supérieur droit de ce graphique en courbes, une fenêtre « Pin tooDashboard » peut s’afficheront vous toochoose un tableau de bord. Sélectionnez EnergyStreamDataReport, puis cliquez sur Épingler.
   * Pointez la souris hello sur cette vignette de tableau de bord hello, cliquez sur « Modifier » icône dans le coin supérieur droit toochange son titre en tant que « À la demande par Timestamp »
4. Créez d’autres vignettes de tableau de bord en fonction des jeux de données appropriés. affichage du tableau de bord final Hello est indiqué ci-dessous.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Configurer le tableau de bord de chemin à froid
Dans le pipeline de données de chemin d’accès à froid, hello essentielles vise à la demande de tooget hello prévision de chaque région. Power BI connecte à base de données SQL Azure tooan comme source de données, où sont stockés les résultats de prédiction hello.

> [!NOTE]
> 1) Il prend quelques heures toocollect suffisamment prévision des résultats pour le tableau de bord hello. Nous vous recommandons de que commencer ce processus 2-3 heures après déjeuner de générateur de données hello. (2) dans cette étape, condition préalable de hello est toodownload et installer le logiciel libre hello [Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Obtenir des informations d’identification de la base de données hello.

   Vous devez **nom du serveur, nom de la base de données, nom d’utilisateur et mot de passe de base de données** avant de déplacer des étapes de toonext. Voici hello étapes tooguide vous comment toofind les.

   * Une fois qu’**Azure SQL Database** apparaît en vert sur votre schéma de modèle de solution, cliquez dessus, puis cliquez sur **Ouvrir**. Vous serez le portail de gestion tooAzure guidée et votre page d’informations de base de données s’ouvre également.
   * Sur la page de hello, vous trouverez une section « Database ». Il indique que vous avez créé une base de données hello. nom de Hello de votre base de données doit être **« Votre nom de la Solution + nombre aléatoire + « db » »** (par exemple, « mytest12345db »).
   * Cliquez sur votre base de données, Bonjour nouveau que POP panneau, vous pouvez trouver le nom de votre serveur de base de données en haut de hello. Le nom de votre base de données doit être au format **"Your Solution Name + Random Number + 'database.windows.net,1433'"** (e.g. "mytest12345.database.windows.net,1433").
   * Votre base de données **nom d’utilisateur** et **mot de passe** sont hello identique hello nom d’utilisateur et mot de passe enregistré précédemment au cours de déploiement de solution de hello.
2. Mettre à jour la source de données hello du chemin d’accès à froid hello fichier Power BI

   * Assurez-vous que vous avez installé la version la plus récente de hello [Power BI desktop](https://powerbi.microsoft.com/desktop).
   * Bonjour **« DemandForecastingDataGeneratorv1.0 »** dossier que vous avez téléchargé, double-cliquez sur hello **'Template\DemandForecastPowerBI.pbix de BI Power'** fichier. les visualisations initiale Hello sont basées sur des données fictives. **Remarque :** si vous voyez une erreur de massage, assurez-vous que vous avez installé la version la plus récente de Power BI Desktop hello.

     Une fois que vous ouvrez, haut hello du fichier de hello, cliquez sur **modifier les requêtes**. Bonjour pop fenêtre, double-cliquez sur **'Source'** sur le panneau droit hello.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * Bonjour pop fenêtre, remplacez **« Server »** et **« Database »** avec vos propres noms de serveur et de base de données, puis cliquez sur **« OK »**. Nom de serveur, veillez à spécifier le port 1433 hello (**YourSolutionName.database.windows.net, 1433**). Ignorer les messages d’avertissement hello qui apparaissent sur l’écran hello.
   * Pop suivant de hello fenêtre, vous voyez deux options dans le volet gauche de hello (**Windows** et **base de données**). Cliquez sur **« Database »**, renseignez vos **« Nom_utilisateur »** et **« Password »** (c’est le nom d’utilisateur hello et mot de passe lorsque vous tout d’abord hello solution déployée et créé un Base de données SQL Azure). Dans ***sélectionnez qui niveau tooapply ces paramètres***, vérifiez l’option de niveau de base de données. Cliquez ensuite sur **Se connecter**.
   * Une fois que vous êtes page précédente de guidée toohello précédent, fermez la fenêtre hello. Un message s’affiche ; cliquez sur **Appliquer**. Enfin, cliquez sur hello **enregistrer** bouton les modifications de hello toosave. Votre fichier Power BI a désormais établi toohello de connexion du serveur. Si vos visualisations sont vides, veillez à que désactiver les sélections de hello sur hello visualisations toovisualize toutes les données hello en cliquant sur icône de gomme hello sur hello coin supérieur droit de légendes de hello. Utiliser hello actualisation bouton tooreflect nouvelles données sur les visualisations hello. Au départ, vous verrez seulement les données de valeur initiale salutation sur vos visualisations comme hello data factory est toorefresh planifiée toutes les 3 heures. Après 3 heures, vous verrez les nouvelles prédictions reflétées dans vos visualisations lorsque vous actualisez les données de salutation.
3. (Facultatif) Publier le tableau de bord de chemin d’accès à froid hello trop[Power BI en ligne](http://www.powerbi.com/). Notez que vous avez besoin d’un compte Power BI (ou d’un compte Office 365) pour cette étape.

   * Cliquez sur **« Publier »** et quelques secondes plus tard une fenêtre s’affiche et indique « Publication tooPower BI succès ! » avec une coche verte. Cliquez sur lien hello sous « Demoprediction.pbix ouvrir dans Power BI ». toofind des instructions, consultez [publier à partir de Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate un tableau de bord : cliquez sur hello  **+**  signer suivant toothe **tableaux de bord** section dans le volet gauche de hello. Entrez le nom hello « À la demande de prévision Demo » pour le nouveau tableau de bord.
   * Une fois que vous ouvrez hello rapport, cliquez sur ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin toutes les visualisations tooyour tableau de bord. toofind des instructions, consultez [épingler un tableau de bord Power BI de tooa vignette à partir d’un rapport](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Atteindre la page de tableau de bord toohello et ajuster la taille de hello et l’emplacement de vos visualisations et modifiez leur titre. toofind des instructions détaillées sur tooedit vos vignettes, voir [modifier un titre--redimensionner, déplacer, renommer, épingler, supprimer, ajouter un lien hypertexte](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Voici un exemple d’un tableau de bord avec certaines tooit de visualisations épinglées de chemin d’accès à froid.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (Facultatif) Planifier l’actualisation de la source de données hello.

   * tooschedule l’actualisation des données de hello, pointez votre souris sur hello **EnergyBPI-Final** jeu de données, cliquez sur ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) , puis **planifier l’actualisation**.
     **Remarque :** si vous voyez un message d’avertissement, cliquez sur **modifier les informations d’identification** et assurez-vous que vos informations d’identification de base de données sont hello identiques à ceux décrits à l’étape 1.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Développez hello **planifier l’actualisation** section. Activez l’option Maintenir vos données à jour.
   * Planifier l’actualisation hello selon vos besoins. toofind plus d’informations, consultez [d’actualisation des données dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**Comment toodelete votre solution**
Veuillez vous assurer que vous arrêtez le Générateur de données hello lorsque vous N'utilisez pas activement des solutions de hello en exécutant le Générateur de données hello entraîne des coûts plus élevés. Si vous ne l’utilisez pas, supprimez les solutions hello. La suppression de votre solution supprimera tous les composants hello configurés dans votre abonnement lorsque vous avez déployé la solution de hello. solution de hello toodelete cliquez sur le nom de votre solution dans le panneau gauche de hello du modèle de solution hello et cliquez sur Supprimer.

## <a name="cost-estimation-tools"></a>**Outils d’estimation des coûts**
Hello deux outils suivants sont disponible toohelp vous de mieux comprendre le coût total en cours d’hello prévision de la demande pour le modèle de Solution de l’énergie dans votre abonnement :

* [Microsoft Azure Cost Estimator Tool (en ligne)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (de bureau)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Remerciements**
Cet article a été créé par le scientifique de données Yijing Chen et l’ingénieur logiciel Min Qiu de Microsoft.
