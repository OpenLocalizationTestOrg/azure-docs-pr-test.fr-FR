---
title: "maintenance aaaPredictive dans aérospatial avec Azure - guide technique de la Solution d’analyse décisionnelle Cortana | Documents Microsoft"
description: "Un guide technique toohello modèle de Solution avec Business Intelligence de Microsoft Cortana pour maintenance prédictive aérospatial et utilitaires de transport."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Guide technique toohello Cortana Intelligence Solution de modèle pour une maintenance prédictive aérospatial et les autres entreprises

## <a name="important"></a>**Important**
Cet article est obsolète. informations de Hello sont toujours applicables toohello problème, autrement dit, la Maintenance prédictive dans aérospatiale, mais se trouve le dernier article de hello avec hello plus les informations de toodate [ici](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Remerciements**
Cet article a été coécrit par les scientifiques de données Yan Zhang, Gauher Shaheen, Fidan Boylu Uz et par l’ingénieur logiciel Dan Grecoe chez Microsoft.

## <a name="overview"></a>**Vue d'ensemble**
Modèles de solution sont conçues tooaccelerate hello consistant à générer une démonstration E2E par-dessus Cortana Intelligence Suite. Un modèle déployé provisionner votre abonnement avec les composants Cortana Intelligence nécessaires et créer des relations de hello entre eux. Il alimente également pipeline de données hello avec des exemples de données générés à partir d’une application de générateur de données qui vous serez également télécharger et installer sur votre ordinateur local après avoir déployé le modèle de solution hello. données Hello générées à partir du Générateur de hello hydrate le pipeline de données hello et commencer à générer des prédictions d’apprentissage automatique qui peuvent ensuite être visualisées dans le tableau de bord Power BI hello. processus de déploiement Hello va vous guider tout au long de plusieurs étapes tooset, vos informations d’identification de la solution. Assurez-vous que vous enregistrez ces informations d’identification telles que le nom de la solution, nom d’utilisateur et mot de passe indiqués au cours du déploiement de hello.  

objectif Hello de ce document est l’architecture de référence tooexplain hello et différents composants configurés dans votre abonnement dans le cadre de ce modèle de solution. document de Hello traite également de la tooreplace les exemples de données avec des données réelles de vos propres toobe toosee en mesure d’insights des prédictions à partir de vos propres données. En outre, les documents hello décrit les parties du modèle de Solution qui doivent toobe modifiée si vous souhaitiez solution de hello toocustomize avec vos propres données de hello. Obtenir des instructions sur la façon dont toobuild hello du tableau de bord Power BI pour ce modèle de Solution sont fournies à la fin de hello.

> [!TIP]
> Vous pouvez télécharger et imprimer une [version PDF de ce document](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Grandes lignes**
![Architecture de maintenance prédictive](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Lors de la solution de hello est déployée, les divers services Azure dans Cortana Analytique Suite sont activés (*par exemple,* Event Hub, Stream Analytics, HDInsight, Data Factory, Machine Learning, *etc.*). diagramme d’architecture Hello ci-dessus montre, à un niveau élevé, comment hello Maintenance prédictive pour le modèle de Solution aérospatial est construit à partir de bout en bout. Vous serez en mesure de tooinvestigate ces services dans le portail hello azure en cliquant dessus dans le diagramme de modèle de solution hello créé avec le déploiement hello de solution de hello avec l’exception hello de HDInsight en tant que ce service est configuré sur demande lorsque hello associées activités de pipeline toorun requis et supprimés par la suite.
Vous pouvez télécharger un [version en taille réelle du diagramme de hello](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Hello les sections suivantes décrire chaque élément.

## <a name="data-source-and-ingestion"></a>**Source et ingestion de données**
### <a name="synthetic-data-source"></a>Source de données de synthèse
Pour ces données de hello du modèle source utilisé est généré à partir d’une application de bureau que vous allez télécharger et exécuter localement après un déploiement réussi. Vous recherchez toodownload d’instructions hello et installer cette application dans la barre des propriétés hello lorsque vous sélectionnez hello premier nœud appelé prédictive Générateur de données de gestion sur le diagramme de modèle de solution hello. Cette application de flux de hello [concentrateur d’événements Azure](#azure-event-hub) service avec des points de données ou des événements, qui seront utilisés dans le reste de hello du flux de solution hello. Cette source de données est constituée d’ou dérivée des données accessibles à partir de la [référentiel de données NASA](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) à l’aide de hello [jeu de données à moteur dégradation Simulation](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

application de la génération des événements Hello remplira hello concentrateur d’événements Azure uniquement lors de son exécution sur votre ordinateur.

### <a name="azure-event-hub"></a>Azure Event Hub
Hello [concentrateur d’événements Azure](https://azure.microsoft.com/services/event-hubs/) service est destinataire hello d’entrée hello fournie par hello synthétique Source de données décrit ci-dessus.

## <a name="data-preparation-and-analysis"></a>**Préparation et analyse des données**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) service est utilisé tooprovide près analytique en temps réel sur les flux d’entrée de hello de hello [concentrateur d’événements Azure](#azure-event-hub) de service et de publier les résultats sur un [Power BI](https://powerbi.microsoft.com) tableau de bord, ainsi que l’archivage de tous les bruts toohello événements entrants [Azure Storage](https://azure.microsoft.com/services/storage/) service pour un traitement ultérieur par hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service.

### <a name="hd-insights-custom-aggregation"></a>Agrégation personnalisée HD Insights
Hello service de Azure HD Insight est utilisé toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) agrégations tooprovide de scripts (orchestrés par Azure Data Factory) sur des événements bruts hello qui ont été archivés à l’aide du service d’Analytique de flux de données Azure hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) service est utilisé (orchestrés par Azure Data Factory) prédictions toomake sur hello restants du cycle de vie (RUL) d’un moteur d’avion particulier donné d’entrées hello reçues.

## <a name="data-publishing"></a>**Publication des données**
### <a name="azure-sql-database-service"></a>Service de base de données SQL Azure
Hello [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/) service est reçues par hello service Azure Machine Learning qui est consommée Bonjour des prédictions de hello toostore utilisé (géré par Azure Data Factory) [Power BI](https://powerbi.microsoft.com) tableau de bord.

## <a name="data-consumption"></a>**Consommation des données**
### <a name="power-bi"></a>Power BI
Hello [Power BI](https://powerbi.microsoft.com) service est tooshow utilisé un tableau de bord qui contient des agrégations et les alertes fournies par hello [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) service, ainsi que les prédictions RUL stockées dans [SQL Azure Base de données](https://azure.microsoft.com/services/sql-database/) qui ont été générés à l’aide de hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) service. Pour obtenir des Instructions sur la façon dont toobuild hello du tableau de bord Power BI pour ce modèle de Solution, consultez la section toohello ci-dessous.

## <a name="how-toobring-in-your-own-data"></a>**Comment toobring vos données**
Cette section décrit comment toobring tooAzure de vos propres données et zones nécessiterait change pour les données de salutation vous amener à cette architecture.

Il est peu probable que vous mettez tout jeu de données correspondrait à hello le jeu de données utilisé par hello [jeu de données à moteur dégradation Simulation](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) utilisé pour ce modèle de solution. Présentation de vos données et la configuration requise sera essentiel dans la façon dont vous modifier toowork de ce modèle avec vos propres données. S’il s’agit de votre première toohello d’exposition service Azure Machine Learning, vous pouvez obtenir un tooit introduction à l’aide d’exemple hello dans [comment toocreate votre première expérience](machine-learning-create-experiment.md).

traite des sections hello du modèle hello qui requièrent des modifications lorsqu’un nouveau jeu de données est introduit Hello les sections suivantes.

### <a name="azure-event-hub"></a>Azure Event Hub
Hello service de concentrateur d’événements Azure est très générique, telles que les données peuvent être publiées toohello hub au format CSV ou JSON. Aucun traitement spécial se produit dans hello concentrateur d’événements Azure, mais il est important de comprendre les données hello qui sont chargées dans celui-ci.

Ce document ne décrit pas comment tooingest vos données, mais vous pouvez envoyer facilement des événements ou à l’aide de données tooan concentrateur d’événements Azure hello API concentrateur d’événements.

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello service d’Analytique de flux de données Azure est utilisé tooprovide près analytique en temps réel par la lecture à partir de flux de données et la sortie des données tooany de diverses sources.

Pour hello Maintenance prédictive pour le modèle de Solution aérospatial, la requête Analytique de flux de données Azure se compose de quatre sous-requêtes, chaque événements consommation hello service de concentrateur d’événements Azure et avoir des sorties à quatre emplacements distincts. Ces sorties comprennent trois jeux de données Power BI et un emplacement Azure Storage.

requête d’Analytique de flux de données Azure Hello sont accessibles via :

* Connectez hello portail Azure
* Localisation des tâches de flux de données Analytique hello ![icône de flux de données Analytique](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) qui ont été générés lors du déploiement de solutions de hello (*par exemple,*, **maintenancesa02asapbi** et **maintenancesa02asablob** pour la solution de maintenance prédictive)
* Sélectionnez
  
  * ***ENTRÉES*** entrée de requête hello tooview
  * ***REQUÊTE*** tooview hello requête
  * ***SORTIES*** tooview hello différentes sorties

Vous trouverez plus d’informations sur la construction de la requête Analytique de flux de données Azure Bonjour [référence de flux de requête Analytique](https://msdn.microsoft.com/library/azure/dn834998.aspx) sur MSDN.

Dans cette solution, les requêtes hello sortie trois jeux de données avec des informations d’analytique en temps réel sur hello entrant données flux tooa tableau de bord qui est fourni dans le cadre de ce modèle de solution presque. Étant donné qu’une connaissance implicite sur le format de données entrants hello, ces requêtes devez toobe modifiée en fonction de votre format de données.

requête Hello dans la deuxième tâche de flux de données Analytique hello **maintenancesa02asablob** simplement génère tous les [concentrateur d’événements](https://azure.microsoft.com/services/event-hubs/) événements [Azure Storage](https://azure.microsoft.com/services/storage/) et ne nécessite donc aucune modification quel que soit votre format de données en tant que hello les informations d’événement complet sont transmis en continu toostorage.

### <a name="azure-data-factory"></a>Azure Data Factory
Hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service orchestre le déplacement des hello et le traitement des données. Dans la Maintenance prédictive pour les données de modèle de Solution aérospatial hello fabrique est constituée de trois [pipelines](../data-factory/data-factory-create-pipelines.md) qui déplacer et traiter les données hello à l’aide de différentes technologies.  Vous pouvez accéder à votre fabrique de données en ouvrant le nœud de fabrique de données hello hello bas hello du diagramme de modèle de solution hello créé avec le déploiement hello de solution de hello. Cette opération prendra vous toohello fabrique de données sur votre portail Azure. Si vous constatez des erreurs dans vos jeux de données, vous pouvez ignorer ceux qu’ils sont en raison de la fabrique de toodata en cours de déploiement avant le démarrage de générateur de données hello. Ces erreurs ne perturbent pas le fonctionnement de votre fabrique de données.

![Erreurs de jeu de données Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

Cette section traite des hello nécessaire [pipelines](../data-factory/data-factory-create-pipelines.md) et [activités](../data-factory/data-factory-create-pipelines.md) contenus dans hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Voici la vue de diagramme hello de solution de hello.

![Azure Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Deux des pipelines hello de cette fabrique contiennent [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts toopartition utilisée et les données d’agrégation hello. Lorsque cela est indiqué, les scripts hello se trouve dans hello [Azure Storage](https://azure.microsoft.com/services/storage/) compte créé pendant l’installation. à l’emplacement suivant : maintenancesascript\\\\script\\\\hive\\\\ (ou https://[nom de votre solution].blob.core.windows.net/maintenancesascript).

Toohello similaire [Analytique de flux de données Azure](#azure-stream-analytics-1) requêtes, le [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts ont une connaissance implicite sur le format de données entrants hello, ces requêtes devez toobe modifiée en fonction de votre format de date et [l’équipe d’ingénierie de fonctionnalité](machine-learning-feature-selection-and-engineering.md) configuration requise.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Cela [pipeline](../data-factory/data-factory-create-pipelines.md) contient une activité unique - une [HDInsightHive](../data-factory/data-factory-hive-activity.md) à l’aide de l’activité une [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) qui exécute un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) placer des données de script toopartition hello dans [Azure Storage](https://azure.microsoft.com/services/storage/) pendant la [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) travail.

Le script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) pour cette tâche de partitionnement est ***AggregateFlightInfo.hql***

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Cela [pipeline](../data-factory/data-factory-create-pipelines.md) contient plusieurs activités et dont le résultat final est prédictions hello au score calculé à partir de hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) expérimentation associée à ce modèle de solution.

les activités Hello contenues dans ce sont :

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) à l’aide de l’activité une [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) qui exécute un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) tooperform agrégations de script et d’une fonctionnalité de l’équipe d’ingénierie nécessaire pour hello [Azure Apprentissage](https://azure.microsoft.com/services/machine-learning/) faire des essais.
  Le script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) pour cette tâche de partitionnement est ***PrepareMLInput.hql***.
* [Copie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activité qui déplace les résultats hello à partir de la [HDInsightHive](../data-factory/data-factory-hive-activity.md) tooa d’activité unique [Azure Storage](https://azure.microsoft.com/services/storage/) objet blob qui est accessibles par le [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) activité.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) activité qui appelle hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) expérience, ce qui entraîne des résultats hello dans un seul [Azure Storage](https://azure.microsoft.com/services/storage/) blob.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Cela [pipeline](../data-factory/data-factory-create-pipelines.md) contient une activité unique - une [copie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activité qui déplace les résultats hello Hello [Azure Machine Learning](#azure-machine-learning) tester à partir de la *** MLScoringPipeline*** toohello [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/) qui a été configuré dans le cadre de l’installation du modèle de solution.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) expérience utilisé pour ce modèle de solution fournit hello restantes utile vie (RUL) un moteur d’avion. expérience de Hello est le jeu de données spécifique toohello consommée et nécessite donc des données spécifiques toohello modification ou de remplacement qui s’affiche dans.

Pour plus d’informations sur la création de hello expérience Azure Machine Learning, consultez [Maintenance prédictive : étape 1 sur 3, la préparation des données et ingénierie de fonctionnalité](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**Surveiller la progression**
 Une fois que hello Générateur de données est lancé, pipeline hello commence tooget intégré et hello différents composants de votre solution démarrent son en action commandes hello émis par hello Data Factory. Il existe deux façons, que vous pouvez surveiller le pipeline de hello.

1. Un des travaux de flux de données Analytique hello écrit hello entrants données tooblob un stockage brut. Si vous cliquez sur dans le composant de stockage d’objets Blob de votre solution à partir de l’écran hello vous hello correctement déployé la solution et puis cliquez sur Ouvrir dans le panneau droit hello, elle prendra vous toohello [portail de gestion](https://portal.azure.com/). Une fois dans le portail, cliquez sur Objets BLOB. Dans le panneau de configuration suivant hello, vous verrez une liste de conteneurs. Cliquez sur **maintenancesadata**. Dans le panneau de configuration suivant hello, vous verrez hello **rawdata** dossier. À l’intérieur du dossier de rawdata hello, vous verrez des dossiers avec des noms comme heure = 17, heure = etc. 18. Si vous voyez ces dossiers, il indique que les données brutes hello sont correctement générée sur votre ordinateur et stockées dans le stockage d’objets blob. Vous devriez voir des fichiers csv avec des tailles finies en Mo dans ces dossiers.
2. Hello dernière étape du pipeline de hello donnée toowrite (par exemple, les prédictions à partir de l’apprentissage) dans la base de données SQL. Vous pouvez avoir toowait un maximum de trois heures hello données tooappear dans base de données SQL. Une façon toomonitor la quantité de données est disponible dans votre base de données SQL s’effectue via [portail azure](https://manage.windowsazure.com/). Sur le panneau gauche hello localiser les bases de données SQL ![icône SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) et cliquez dessus. Recherchez ensuite votre base de données **pmaintenancedb** et cliquez dessus. Dans la page suivante de hello bas hello, cliquez sur Gérer
   
    ![Icône Gérer](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    Ici, vous pouvez cliquer sur Nouvelle requête et de requête pour le nombre de hello de lignes (par exemple, select count à partir de PMResult). À mesure que votre base de données augmente, nombre de hello de lignes dans la table de hello doit augmenter.

## <a name="power-bi-dashboard"></a>**Tableau de bord Power BI**
### <a name="overview"></a>Vue d'ensemble
Cette section décrit comment tooset des toovisualize du tableau de bord Power BI vos données en temps réel à partir d’Azure Stream Analytique (chemin d’accès à chaud), ainsi que la prédiction par lot résultant apprentissage Azure (chemin d’accès à froid).

### <a name="setup-cold-path-dashboard"></a>Configuration du tableau de bord de chemin à froid
Dans le pipeline de données de chemin d’accès à froid hello, hello essentielles vise tooget le RUL prédictive (restante cycle de vie) du moteur de chaque appareil une fois qu’il termine un vol (cycle). résultat de prédiction Hello est mise à jour toutes les 3 heures pour la prédiction de moteurs hello qui ont passé un vol pendant hello passées 3 heures.

Power BI connecte à base de données SQL Azure tooan comme source de données, où sont stockés les résultats de prédiction. Remarque : 1) au moment de déployer votre solution, une prédiction réelle s’afficheront dans la base de données hello dans les 3 heures.
fichier pbix Hello fournie avec le téléchargement du générateur hello contient des données de valeur initiale afin que vous pouvez créer des tableaux de bord Power BI hello immédiatement. (2) dans cette étape, condition préalable de hello est toodownload et installer le logiciel libre hello [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Hello suit vous guide sur comment tooconnect hello pbix fichier Hello de base de données SQL qui a été lancé au moment de hello du déploiement d’une solution contenant des données (*, par exemple*. résultats de prédiction) pouvant être visualisées.

1. Obtenir des informations d’identification de la base de données hello.
   
   Vous devez **nom du serveur, nom de la base de données, nom d’utilisateur et mot de passe de base de données** avant de déplacer des étapes de toonext. Voici hello étapes tooguide vous comment toofind les.
   
   * Une fois qu’**Azure SQL Database** apparaît en vert sur votre schéma de modèle de solution, cliquez dessus, puis cliquez sur **Ouvrir**.
   * Vous verrez une nouvel onglet/fenêtre de navigateur qui affiche hello page du portail Azure. Cliquez sur **« Groupes de ressources »** sur le panneau gauche hello.
   * Sélectionnez abonnement hello vous utilisez pour le déploiement de solutions de hello, puis **' Nom_solution\_le groupe de ressources '**.
   * Dans hello nouveau pop panneau, cliquez sur hello ![icône SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) icône tooaccess votre base de données. Le nom de votre base de données est toohello suivant cette icône (*par exemple,*, **'pmaintenancedb'**) et hello **nom du serveur de base de données** est répertorié sous hello propriété de nom de serveur et doit se présenter similaire trop**YourSoutionName.database.windows.net**.
   * Votre base de données **nom d’utilisateur** et **mot de passe** sont hello identique hello nom d’utilisateur et mot de passe enregistré précédemment au cours de déploiement de solution de hello.
2. Mettre à jour la source de données hello hello à froid de chemin d’accès du fichier de rapport Power BI Desktop.
   
   * Dans le dossier hello sur votre ordinateur où vous avez téléchargé et que vous avez décompressé le fichier de générateur, double-cliquez sur le **PowerBI\\PredictiveMaintenanceAerospace.pbix** fichier. Si vous consultez les messages d’avertissement lorsque vous ouvrez le fichier de hello, les ignorer. En haut de hello du fichier de hello, cliquez sur **modifier les requêtes**.
     
     ![Modifier les requêtes](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Deux tables apparaissent : **RemainingUsefulLife** et **PMResult**. Sélectionnez la première table de hello et cliquez sur ![icône des paramètres de requête](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) suivant trop**'Source'** sous **'Étapes appliquées'** sur hello droit **'Paramètres de requête'**Panneau de configuration. Ignorer les messages d’avertissement qui s’affichent.
   * Bonjour pop fenêtre, remplacez **'Server'** et **'Database'** avec vos propres noms de serveur et de base de données, puis cliquez sur **'OK'**. Nom de serveur, veillez à spécifier le port 1433 hello (**YourSoutionName.database.windows.net, 1433**). Laissez le champ de base de données hello en tant que **pmaintenancedb**. Ignorer les messages d’avertissement hello qui apparaissent sur l’écran hello.
   * Pop suivant de hello fenêtre, vous voyez deux options dans le volet gauche de hello (**Windows** et **base de données**). Cliquez sur **'Database'**, renseignez vos **'Nom_utilisateur'** et **'Password'** (c’est le nom d’utilisateur hello et mot de passe lorsque vous tout d’abord hello solution déployée et créé un Base de données SQL Azure). Dans ***sélectionnez qui niveau tooapply ces paramètres***, vérifiez l’option de niveau de base de données. Cliquez ensuite sur **Se connecter**.
   * Cliquez sur la table de deuxième hello **PMResult** puis cliquez sur ![icône de Navigation](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) suivant trop**'Source'** sous **'Étapes appliquées'** sur hello droite **'Paramètres de requête'** panneau et mettre à jour hello nom du serveur et base de données comme dans hello étapes ci-dessus et cliquez sur OK.
   * Une fois que vous êtes page précédente de guidée toohello précédent, fermez la fenêtre hello. Un message s’affiche ; cliquez sur **Appliquer**. Enfin, cliquez sur hello **enregistrer** bouton les modifications de hello toosave. Votre fichier Power BI a désormais établi toohello de connexion du serveur. Si vos visualisations sont vides, veillez à que désactiver les sélections de hello sur hello visualisations toovisualize toutes les données hello en cliquant sur icône de gomme hello sur hello coin supérieur droit de légendes de hello. Utiliser hello actualisation bouton tooreflect nouvelles données sur les visualisations hello. Au départ, vous verrez seulement les données de valeur initiale salutation sur vos visualisations comme hello data factory est toorefresh planifiée toutes les 3 heures. Après 3 heures, vous verrez les nouvelles prédictions reflétées dans vos visualisations lorsque vous actualisez les données de salutation.
3. (Facultatif) Publier le tableau de bord de chemin d’accès à froid hello trop[Power BI en ligne](http://www.powerbi.com/). Notez que vous avez besoin d’un compte Power BI (ou d’un compte Office 365) pour cette étape.
   
   * Cliquez sur **« Publier »** et quelques secondes plus tard une fenêtre s’affiche et indique « Publication tooPower BI succès ! » avec une coche verte. Cliquez sur lien hello sous « PredictiveMaintenanceAerospace.pbix ouvrir dans Power BI ». toofind des instructions, consultez [publier à partir de Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate un tableau de bord : cliquez sur hello  **+**  signer suivant toothe **tableaux de bord** section dans le volet gauche de hello. Entrez le nom hello « Demo de Maintenance prédictive » pour le nouveau tableau de bord.
   * Une fois que vous ouvrez hello rapport, cliquez sur ![icône d’épingle](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin toutes les visualisations tooyour tableau de bord. toofind des instructions, consultez [épingler un tableau de bord Power BI de tooa vignette à partir d’un rapport](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Atteindre la page de tableau de bord toohello et ajuster la taille de hello et l’emplacement de vos visualisations et modifiez leur titre. toofind des instructions détaillées sur tooedit vos vignettes, voir [modifier un titre--redimensionner, déplacer, renommer, épingler, supprimer, ajouter un lien hypertexte](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Voici un exemple d’un tableau de bord avec certaines tooit de visualisations épinglées de chemin d’accès à froid.  Selon la durée pendant laquelle vous exécutez votre générateur de données, vos numéros de visualisations de hello peut être différent.
     <br/>
     ![Affichage final](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * tooschedule l’actualisation des données de hello, pointez votre souris sur hello **PredictiveMaintenanceAerospace** jeu de données, cliquez sur ![des points de suspension icône](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) , puis **planifier l’actualisation**.
     <br/>
     **Remarque :** si vous voyez un message d’avertissement, cliquez sur **modifier les informations d’identification** et assurez-vous que vos informations d’identification de base de données sont hello identiques à ceux décrits à l’étape 1.
     <br/>
     ![Planifier l’actualisation](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Développez hello **planifier l’actualisation** section. Activez l’option Maintenir vos données à jour.
     <br/>
   * Planifier l’actualisation hello selon vos besoins. toofind plus d’informations, consultez [d’actualisation des données dans Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Configuration du tableau de bord de chemin à chaud
vous guide Hello suit comment toovisualize en temps réel de sortie de données à partir de l’Analytique des flux de travaux qui ont été générées au moment de hello du déploiement de la solution. A [Power BI en ligne](http://www.powerbi.com/) compte est hello tooperform requis comme suit. Si vous ne possédez pas de compte, vous pouvez en [créer un](https://powerbi.microsoft.com/pricing).

1. Ajouter une sortie Power BI dans Azure Stream Analytics (ASA).
   
   * Vous devez obtenir des instructions de hello toofollow dans [Analytique de flux de données Azure et Power BI : un tableau de bord analytique en temps réel pour la visibilité en temps réel des flux de données](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset de sortie hello de votre travail Analytique des flux de données Azure en tant que votre puissance Tableau de bord BI.
   * requête ASA Hello possède trois sorties qui sont **aircraftmonitor**, **aircraftalert**, et **flightsbyhour**. Vous pouvez afficher la requête de hello en cliquant sur l’onglet requête. Tooeach correspondante de ces tables, vous devez tooadd une tooASA de sortie. Lorsque vous ajoutez la première sortie de hello (*par exemple,* **aircraftmonitor**) Vérifiez que hello **Alias de sortie**, **nom du Dataset** et  **Nom de la table** sont hello même (**aircraftmonitor**). Sorties hello répétition étapes tooadd **aircraftalert**, et **flightsbyhour**. Une fois que vous avez ajouté tous les trois tables de sortie et hello ASA tâche démarrée, vous devez obtenir un message de confirmation (*, par exemple*, « Analytique de flux de données de départ de la tâche maintenancesa02asapbi a réussi »).
2. Connectez-vous trop[Power BI en ligne](http://www.powerbi.com)
   
   * Sur hello gauche Panneau de configuration des groupes de données dans mon espace de travail, le ***DATASET*** noms **aircraftmonitor**, **aircraftalert**, et **flightsbyhour**doit apparaître. Il s’agit de hello de diffusion en continu de données vous transférées à partir de l’Analytique des flux de données Azure hello précédente step.hello DataSet **flightsbyhour** n’apparaîtra pas à hello même moment que hello autres deux jeux de données en raison de la nature de toohello de requête SQL hello à partir de Il s’agit. Toutefois, il doit s’afficher après une heure.
   * Vérifiez que hello ***visualisations*** volet est ouvert et qu’il est affiché sur le côté droit de l’écran hello.
3. Une fois que vous avez données hello transférée dans Power BI, vous pouvez commencer à visualiser hello de diffusion en continu de données. Voici qu'un exemple tableau de bord avec des visualisations chemin réactif épinglé tooit. Vous pouvez créer d’autres vignettes de tableau de bord en fonction des jeux de données appropriés. Selon la durée pendant laquelle vous exécutez votre générateur de données, vos numéros de visualisations de hello peut être différent.

    ![Vue du tableau de bord](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Voici certains toocreate suit une des vignettes hello ci-dessus : hello « vue flotte de capteur 11 vs. Threshold 48.26 » :
   
   * Cliquez sur le dataset **aircraftmonitor** sur hello section des jeux de données du Panneau de gauche.
   * Cliquez sur hello **graphique en courbes** icône.
   * Cliquez sur **traités** Bonjour **champs** volet afin qu’elle s’affiche sous « Axe » Bonjour **visualisations** volet.
   * Cliquez sur « s11 » et « s11alert\_alert » pour faire apparaître les deux sous « Valeurs ». Cliquez sur flèche hello suivant trop**F11** et **F11\_alerte**, modifiez « Sum » trop « moyenne ».
   * Cliquez sur **enregistrer** hello haut et nommez les rapports hello « aircraftmonitor ». Le rapport nommé « aircraftmonitor » s’affichera dans hello **rapports** section Bonjour **Navigator** volet à gauche de hello.
   * Cliquez sur hello **Pin Visual** icône sur hello haut à droite de ce graphique en courbes. Une fenêtre « Pin tooDashboard » peut apparaître pour vous permettre de choisir un tableau de bord. Sélectionnez « Démo de Maintenance prédictive », puis cliquez sur « Épingler ».
   * Placez le curseur de la souris hello sur cette vignette sur le tableau de bord hello, cliquez sur icône du « edit » hello sur hello coin supérieur droit toochange son titre trop « vs flotte vue de capteur 11. Seuil 48,26" et le sous-titre trop « moyenne entre flotte au fil du temps ».

## <a name="how-toodelete-your-solution"></a>**Comment toodelete votre solution**
Veuillez vous assurer que vous arrêtez le Générateur de données hello lorsque vous N'utilisez pas activement des solutions de hello en exécutant le Générateur de données hello entraîne des coûts plus élevés. Si vous ne l’utilisez pas, supprimez les solutions hello. La suppression de votre solution supprimera tous les composants hello configurés dans votre abonnement lorsque vous avez déployé la solution de hello. solution de hello toodelete cliquez sur le nom de votre solution dans le panneau gauche de hello du modèle de solution hello et cliquez sur Supprimer.

## <a name="cost-estimation-tools"></a>**Outils d’estimation des coûts**
Hello deux outils suivants sont disponible toohelp vous de mieux comprendre le coût total en cours d’hello Maintenance prédictive pour le modèle de Solution aérospatial dans votre abonnement :

* [Microsoft Azure Cost Estimator Tool (en ligne)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (de bureau)](http://www.microsoft.com/download/details.aspx?id=43376)

