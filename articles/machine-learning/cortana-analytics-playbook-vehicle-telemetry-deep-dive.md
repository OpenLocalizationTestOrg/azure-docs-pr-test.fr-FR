---
title: "aaaDeep approfondir prédire l’intégrité du véhicule et du pilotage habitudes - Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de hello des aperçus Cortana Intelligence toogain prédictives et en temps réel sur l’intégrité du véhicule et du pilotage habituelles."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Scénario de solution véhicule télémétrie analytique : présentation approfondie d’une solution de hello
Cela **menu** lie toohello des sections de ce manuel : 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Cette section permet d’Explorer chacune des étapes hello mentionnés dans hello Architecture de Solution avec des instructions et des pointeurs pour la personnalisation. 

## <a name="data-sources"></a>Sources de données
solution de Hello utilise deux sources de données différentes :

* **jeu de données de diagnostic et de signaux des véhicules simulés** et 
* **catalogue de véhicules**

Un simulateur de télématique des véhicules est intégré à cette solution. Il émet des informations de diagnostic et signale l’état toohello correspondant du véhicule de hello et toohello gérant le modèle à un moment donné dans le temps. Cliquez sur [véhicule télématique simulateur](http://go.microsoft.com/fwlink/?LinkId=717075) hello de toodownload **véhicule télématique simulateur Solution Visual Studio** pour les personnalisations en fonction de vos besoins. catalogue de véhicule Hello contient un dataset de référence avec un mappage de toomodel VIN.

![Simulateur de télématique des véhicules](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Figure 1 – Simulateur de télématique des véhicules*

Il s’agit d’un jeu de données au format JSON qui contient les hello suivant le schéma.

| Colonne | Description | Valeurs |
| --- | --- | --- |
| VIN |Numéro d’identification du véhicule généré de manière aléatoire |Ce numéro est obtenu à partir d’une liste de référence contenant 10 000 numéros d’identification de véhicule générés de manière aléatoire. |
| Outside temperature |Hello en dehors de la température où véhicule de hello est conduite |Nombre généré de manière aléatoire et compris entre 0 et 100 |
| Engine temperature |température du moteur Hello du véhicule de hello |Nombre généré de manière aléatoire et compris entre 0 et 500 |
| Vitesse |vitesse du moteur Hello à quels hello véhicule est conduite |Nombre généré de manière aléatoire et compris entre 0 et 100 |
| Fuel |niveau de carburant Hello du véhicule de hello |Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau de carburant en pourcentage) |
| EngineOil |niveau de pétrole Hello du moteur du véhicule de hello |Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau d’huile moteur en pourcentage) |
| Pression des pneus |pression des pneus Hello du véhicule de hello |Nombre généré de manière aléatoire et compris entre 0 et 50 (indique le niveau de pression des pneus en pourcentage) |
| Odometer |kilométrique Hello du véhicule de hello |Nombre généré de manière aléatoire et compris entre 0 et 200 000 |
| Accelerator_pedal_position |position de pédales accélérateur Hello du véhicule de hello |Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau d’accélération en pourcentage) |
| Parking_brake_status |Indique si la récupération du véhicule hello est parqué ou non |True ou False |
| Headlamp_status |Indique où projecteur de hello est activé ou non |True ou False |
| Brake_pedal_status |Indique si les pédales de frein hello est enfoncé ou non |True ou False |
| Transmission_gear_position |position de vitesse de transmission de Hello d’hello véhicule |États : première, deuxième, troisième, quatrième, cinquième, sixième, septième, huitième |
| Ignition_status |Indique si la récupération du véhicule hello est en cours d’exécution ou arrêté |True ou False |
| Windshield_wiper_status |Indique si essuie-glace hello est activé ou non |True ou False |
| ABS |Indique si l’ABS est activé ou non |True ou False |
| Timestamp |horodatage Hello lors de la création du point de données hello |Date |
| City |emplacement de Hello du véhicule de hello |4 villes dans cette solution : Bellevue, Redmond, Sammamish, Seattle |

dataset de référence du modèle Hello véhicule contient un mappage toohello VIN. 

| VIN | Modèle |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Berline |
| 8J0U8XCPRGW4Z3NQE |Hybride |
| WORG68Z2PLTNZDBI7 |Berline familiale |
| JTHMYHQTEPP4WBMRN |Berline |
| W9FTHG27LZN1YWO0Y |Hybride |
| MHTP9N792PHK08WJM |Berline familiale |
| EI4QXI2AXVQQING4I |Berline |
| 5KKR2VB4WHQH97PF8 |Hybride |
| W9NSZ423XZHAONYXB |Berline familiale |
| 26WJSGHX4MA5ROHNL |Cabriolet |
| GHLUB6ONKMOSI7E77 |Break |
| 9C2RHVRVLMEJDBXLP |Voiture compacte |
| BRNHVMZOUJ6EOCP32 |Petit SUV |
| VCYVW0WUZNBTM594J |Voiture de sport |
| HNVCE6YFZSA5M82NY |SUV de taille moyenne |
| 4R30FOR7NUOBL05GJ |Break |
| WYNIIY42VKV6OQS1J |Grand SUV |
| 8Y5QKG27QET1RBK7I |Grand SUV |
| DF6OX2WSRA6511BVG |Coupé |
| Z2EOZWZBXAEW3E60T |Berline |
| M4TV6IEALD5QDS3IR |Hybride |
| VHRA1Y2TGTA84F00H |Berline familiale |
| R0JAUHT1L1R3BIKI0 |Berline |
| 9230C202Z60XX84AU |Hybride |
| T8DNDN5UDCWL7M72H |Berline familiale |
| 4WPYRUZII5YV7YA42 |Berline |
| D1ZVY26UV2BFGHZNO |Hybride |
| XUF99EW9OIQOMV7Q7 |Berline familiale |
| 8OMCL3LGI7XNCC21U |Cabriolet |
| ……. | |

### <a name="references"></a>Références
[Solution Vehicle Telematics Simulator Visual Studio](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Hub d'événement d'Azure](https://azure.microsoft.com/services/event-hubs/)

[Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Ingestion
Combinaisons d’Azure Event Hubs, flux de données Analytique et Data Factory sont optimisées tooingest hello véhicule des signaux, événements de diagnostic hello et en temps réel et analytique du lot. Tous ces composants sont créés et configurés en tant que partie du déploiement d’une solution hello. 

### <a name="real-time-analysis"></a>Analyse en temps réel
Hello les événements générés par hello véhicule télématique simulateur sont publiés à l’aide du concentrateur d’événements toohello hello SDK de concentrateur d’événements. tâche de flux de données Analytique Hello reçoit ces événements à partir de hello concentrateur d’événements et processus hello des données dans le contrôle d’intégrité du véhicule hello tooanalyze en temps réel. 

![Tableau de bord Event Hub](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Figure 4 - Tableau de bord Event Hub*

![Données de traitement de la tâche Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Figure 5 - Données de traitement de la tâche Stream Analytics*

tâche de flux de données Analytique Hello ;

* reçoit des données à partir de hello concentrateur d’événements 
* effectue une jointure avec hello référence toomap hello véhicule VIN toohello correspondante modèle de données 
* conserve les données dans le stockage Blob Azure pour une analyse en mode batch approfondie. 

Hello suivant la requête de flux de données Analytique donnée utilisé toopersist hello dans le stockage d’objets blob Azure. 

![Requête de tâche Stream Analytics pour l’ingestion de données](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Figure 6 - Requête de tâche Stream Analytics pour l’ingestion de données*

### <a name="batch-analysis"></a>Analyse en mode batch
Nous allons également générer un volume supplémentaire de signaux de véhicules simulés ainsi qu’un jeu de données de diagnostic pour permettre une analyse en mode batch approfondie. Il s’agit d’un volume de données représentatif pour le traitement par lots de tooensure requis. Pour cela, nous utilisons un pipeline nommé « PrepareSampleDataPipeline » dans toogenerate de flux de travail Azure Data Factory hello année une de signaux de véhicule simulé et de jeu de données de diagnostic. Cliquez sur [activité personnalisée de Data Factory](http://go.microsoft.com/fwlink/?LinkId=717077) hello de toodownload l’activité personnalisée DotNet solution Visual Studio pour les personnalisations de fabrique de données selon vos besoins. 

![Préparer des exemples de données pour le workflow de traitement par lots](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Figure 7 - Préparer des exemples de données pour le workflow de traitement par lots*

pipeline de Hello se compose de définition d’application .net personnalisée activité, afficher ici :

![Activité PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Figure 8 - PrepareSampleDataPipeline*

Une fois que hello pipeline exécute avec succès et le jeu de données « RawCarEventsTable » est marqué comme « Prêt », un an intéressant de signaux du véhicule simulé et diagnostic les données sont produites. Hello suivante créée dans votre compte de stockage sous le conteneur de « connectedcar » hello de fichiers et de dossiers :

![Sortie de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Figure 9 - Sortie de PrepareSampleDataPipeline*

### <a name="references"></a>Références
[Kit Azure Event Hub SDK pour la réception de flux](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Fonctionnalités de déplacement de données Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)

[Solution Azure Data Factory DotNet Activity Visual Studio pour la préparation des exemples de données](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>Jeu de données de partition hello
Hello brut véhicule semi-structurées signaux et le jeu de données de diagnostic sont partitionnées à l’étape de préparation des données hello dans un format année/mois. Ce partitionnement promeut une interrogation plus efficace et évolutif stockage à long terme en activant la panne d’un basculement à partir d’un objet blob compte toohello ensuite en tant que compte de première hello est saturé. 

>[!NOTE] 
>Cette étape de la solution de hello est le traitement de toobatch uniquement applicable.

Gestion des données d’entrée et de sortie :

* Hello **les données de sortie** (étiqueté *PartitionedCarEventsTable*) est toobe conservée pendant une longue période de temps en tant que formulaire de base / « rawest » hello des données dans « Data Lake « hello client. 
* Hello **les données d’entrée** toothis pipeline serait éliminée généralement en tant que données de sortie hello ont toohello une fidélité optimale d’entrée - il est stocké uniquement (partitionnée) mieux pour une utilisation ultérieure.

![Workflow Partition Car Events](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Figure 10 - Workflow Partition Car Events*

les données brutes Hello sont partitionnées à l’aide d’une activité de la ruche de HDInsight dans « PartitionCarEventsPipeline ». données d’exemple Hello générées à l’étape 1 pour une année sont partitionnées par année/mois. les partitions de Hello sont utilisées toogenerate véhicule signaux et les données de diagnostic pour chaque mois (12 partitions au total) d’une année. 

![Activité PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Figure 11 - PartitionCarEventsPipeline*

***Script Hive PartitionConnectedCarEvents***

Hello script Hive suivant, nommé « partitioncarevents.hql », est utilisé pour le partitionnement et se trouve dans le dossier « \demo\src\connectedcar\scripts » hello hello téléchargé zip. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.

![Sortie partitionnée](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Figure 12 - Sortie partitionnée*

les données de salutation est maintenant optimisée, est plus facile à gérer et prêt pour traitement insights de lot riche toogain. 

## <a name="data-analysis"></a>Analyse des données
Dans cette section, vous voyez comment toocombine Analytique de flux de données Azure, Azure Machine Learning, Azure Data Factory et Azure HDInsight pour enrichi avancé analytique sur l’intégrité du véhicule et du pilotage habituelles. Elle est divisée en trois sous-sections :

1. **Apprentissage**: cette sous-section contient des informations sur l’expérience de détection d’anomalie hello que nous avons utilisé dans cette solution toopredict véhicule maintenance véhicules nécessitant des rappels en raison de problèmes de toosafety et maintenance.
2. **Analyse en temps réel**: cette sous-section contient des informations concernant analytique en temps réel hello à l’aide de hello langage de requête Analytique de flux et Opérationnalisation apprentissage hello faire des essais en temps réel à l’aide d’une application personnalisée.
3. **Analyse du lot**: cette sous-section contient des informations hello transformation et le traitement des données de traitement par lots de hello à l’aide d’Azure HDInsight et Azure Machine Learning mis par Azure Data Factory.

### <a name="machine-learning"></a>Machine Learning
Notre objectif ici est véhicules hello toopredict qui nécessitent une maintenance ou rappel, en fonction de certaines statistiques de contrôle d’intégrité. Nous faisons hello suivant hypothèses

* Si un des hello trois conditions suivantes est remplie, les véhicules hello nécessitent **maintenance maintenance**:
  
  * La pression des pneus faible
  * Le niveau d’huile moteur est faible
  * La température du moteur est élevée
* Si l’une des conditions suivantes de hello est true, les véhicules hello peuvent avoir un **problème de sécurité** et nécessitent **rappel**:
  
  * La température du moteur est élevée mais la température extérieure est faible
  * La température du moteur est faible mais la température extérieure est élevée

Selon les exigences précédentes hello, nous avons créé des anomalies de toodetect deux modèles séparés, un pour la détection de maintenance véhicule et un pour la détection de rappel véhicule. Dans ces deux modèles, algorithme d’analyse du composant Principal (PCA) intégré hello est utilisé pour la détection d’anomalie. 

**Modèle de détection de maintenance**

Si un des trois indicateurs de pression des pneus, pétrole du moteur ou température moteur - satisfait à sa condition respectif, modèle de détection de maintenance hello signale une anomalie. Par conséquent, nous avons besoin uniquement tooconsider ces trois variables de la création du modèle de hello. Dans notre expérience dans Azure Machine Learning, nous avons tout d’abord utiliser un **sélectionner les colonnes dans le jeu de données** module tooextract ces trois variables. Ensuite, nous utilisons modèle de détection d’anomalie module toobuild hello hello d’anomalie basée sur l’ACP détection. 

Analyse des composants principaux (PCA) est une technique d’apprentissage automatique qui peut être appliqué toofeature la détection d’anomalies, la classification et la sélection. PCA convertit un ensemble de cas contenant des variables potentiellement corrélées en un ensemble de valeurs appelées composants principaux. idée de clé Hello de modélisation basés sur l’ACP est tooproject des données sur un espace 3D inférieur afin que les fonctionnalités et les anomalies peuvent être plus facilement identifiables.

Pour chaque nouvelle entrée hello trop de modèle de détection, détecteur d’anomalie de hello calcule d’abord sa projection sur des vecteurs propres de hello, et puis calcule hello normalisée erreur de reconstruction. Cette erreur normalisée est score d’anomalie hello. Erreur de hello Hello supérieur, hello anormale hello instance est. 

Problème de détection de maintenance hello, chaque enregistrement peut être considéré comme un point dans un espace 3D défini par pression des pneus pétrole de moteur et la température du moteur coordonnées. toocapture ces anomalies, nous pouvons hello d’origine données projet dans un espace 3D hello sur un espace de 2 dimensions à l’aide de l’ACP. Par conséquent, nous avons défini le paramètre hello nombre de composants toouse dans l’ACP toobe 2. Ce paramètre joue un rôle important dans l’application de la détection d’anomalies basée sur l’algorithme PCA. Une fois les données projetées à l’aide de PCA, nous pouvons identifier plus facilement ces anomalies.

**Modèle de détection d’anomalie de rappel** dans le modèle de détection d’anomalies hello rappel, nous utilisons hello sélectionner les colonnes dans le jeu de données et d’anomalies basé sur l’ACP modules de détection de la même façon. Plus précisément, nous avons tout d’abord extraire trois variables - température du moteur, la température en dehors et vitesse - à l’aide de hello **sélectionner les colonnes dans le jeu de données** module. Nous avons également inclure la vitesse hello variable étant donné que la température du moteur hello est généralement mis en corrélation toohello vitesse. Ensuite, nous utilisons les données hello tooproject du module de détection d’anomalie basée sur l’ACP d’espace 3D de hello sur un espace de 2 dimensions. critères de rappel Hello sont satisfaites et véhicule de hello exige rappel lors de la température du moteur et température extérieure sont hautement négativement corrélés. À l’aide d’algorithme de détection d’anomalie basée sur l’ACP, nous pouvons capturer les anomalies hello après avoir effectué l’ACP. 

Lors de l’apprentissage d’un modèle, nous devons toouse données normales, qui ne nécessitent pas de maintenance ou rappel en tant que modèle de détection d’anomalie basée sur l’ACP hello des données d’entrée tootrain hello. Bonjour expérience de score, nous utilisons hello formé d’anomalie détection modèle toodetect véhicule de hello nécessite la maintenance ou rappel ou non. 

### <a name="real-time-analysis"></a>Analyse en temps réel
Hello suivant du flux de données Analytique la requête SQL est utilisé moyenne de hello tooget de toutes les hello paramètres véhicule importantes telles que la vitesse du véhicule, niveau de carburant, température du moteur, kilométrique, la pression des pneus, au niveau du moteur pétrole et d’autres. Hello moyennes sont utilisées toodetect anomalies, émettre des alertes et déterminer hello des conditions de contrôle d’intégrité global de véhicules utilisés dans une région spécifique et le corréler puis toodemographics. 

![Requête Stream Analytics pour le traitement en temps réel](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Figure 13 - Requête Stream Analytics pour le traitement en temps réel*

Toutes les moyennes de hello sont calculés sur un TumblingWindow de 3 secondes. Nous utilisons TubmlingWindow dans ce cas car nous avons besoin d’intervalles de temps contigus et sans chevauchement. 

toolearn en savoir plus sur toutes les fonctionnalités de « Fenêtrage » hello dans Azure Analytique de flux de données, cliquez sur [fenêtrage (Analytique de flux de données Azure)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Prédiction en temps réel**

Une application est incluse dans le cadre du modèle d’apprentissage de solution toooperationalize hello hello en temps réel. Cette application appelée « RealTimeDashboardApp » est créée et configurée en tant que partie du déploiement d’une solution hello. application Hello exécute des actions suivantes de hello :

1. Écoute l’instance de concentrateur d’événements tooan où Analytique de flux de données est événements de publication hello dans un modèle en permanence. ![Requête Analytique de flux de données pour la publication des données de salutation](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 : requête Analytique de flux de données pour la publication hello données tooan instance de concentrateur d’événements de sortie* 
2. Pour chaque événement reçu par cette application : 
   
   * Traite les données hello à l’aide du point de terminaison de Machine Learning demande-réponse de calcul de score (RR). point de terminaison RR Hello est automatiquement publié dans le cadre du déploiement de hello.
   * sortie d’enregistrements de ressources Hello est publié tooa jeu de données de Power BI à l’aide de push de hello API.

Ce modèle est également applicable tooscenarios dans lequel vous souhaitez toointegrate une application métier (LoB) avec un flux hello analytique en temps réel, des scénarios tels que des alertes, notifications et la messagerie.

Cliquez sur [RealtimeDashboardApp téléchargement](http://go.microsoft.com/fwlink/?LinkId=717078) hello de toodownload solution RealtimeDashboardApp Visual Studio pour les personnalisations. 

**tooexecute hello Application de tableau de bord en temps réel**
1. Extrayez le fichier et enregistrez-le localement ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – Dossier RealtimeDashboardApp*  
2. Exécutez l’application hello RealtimeDashboardApp.exe
3. Entrez des informations d’identification Power BI valides, connectez-vous, puis cliquez sur Accept ![Application de tableau de bord en temps réel connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Application de tableau de bord en temps réel terminer connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Figure 17 – RealtimeDashboardApp : Connectez-vous tooPower BI*

>[!NOTE] 
>Si vous souhaitez que le jeu de données Power BI tooflush hello, exécutez hello RealtimeDashboardApp avec le paramètre « flushdata » hello : 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Analyse en mode batch
Hello ici vise tooshow comment Contoso auto utilise hello calcul Azure fonctionnalités tooharness données big toogain un éclairage sur gérant le modèle, le comportement de l’utilisation et d’intégrité du véhicule. Il est ainsi possible :

* Améliorer l’expérience utilisateur hello et la rendre plus économique en fournissant des analyses sur la conduite des habitudes et les comportements de conduite efficace de carburant
* En savoir plus proactive concernant les clients et leurs décisions toogovern connues conduite et fournir hello mieux classe produits et services

Dans cette solution, nous prévoyons hello suivant des métriques :

1. **Agressif gèrent le comportement**: identifie la tendance de hello des modèles de hello, des emplacements, déterminant conditions et temps d’aperçus de toogain année hello sur les modèles de conduite agressives. Contoso Motors peut utiliser ces informations pour ses campagnes marketing, pour créer de nouvelles fonctionnalités personnalisées et pour proposer des assurances adaptées à l’utilisation.
2. **Comportement de conduite efficace de carburant**: identifie tendance hello de modèles de hello, emplacements, déterminant conditions et de temps d’aperçus de toogain année hello sur les modèles de conduite efficace de carburant. Moteurs de Contoso peut utiliser ces aperçus pour les campagnes marketing gérant les nouvelles fonctionnalités et proactive reporting toohello pilotes coûtent effectif et environnement convivial conduite des habitudes. 
3. **Modèles de rappeler**: identifie les modèles nécessiter des rappels d’expérience d’apprentissage de la détection d’anomalie hello à mettre en application

Nous allons examiner en détail chacune de ces métriques, hello

**Mode de conduite agressive**

Hello partitionnée véhicule signaux et les données de diagnostic sont traitées dans le pipeline de hello nommé « AggresiveDrivingPatternPipeline » à l’aide de modèles de ruche toodetermine hello, l’emplacement, véhicule, véhicule conditions et autres paramètres qui expose agressif modèle de commande.

![Workflow de modèle conduite agressive](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Workflow de modèle conduite agressive*


***Requête Hive de mode de conduite agressive***

Hello script Hive nommé « aggresivedriving.hql » est utilisé pour analyser le modèle de condition déterminant agressif se trouve dans le dossier « \demo\src\connectedcar\scripts » de hello téléchargé zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Elle utilise la combinaison hello du véhicule position de vitesse de transmission, état pédales de frein et vitesse toodetect reckless/agressif gèrent le comportement en fonction de frein modèle à grande vitesse. 

Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.

![Sortie AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Figure 19 – Sortie AggressiveDrivingPatternPipeline*

**Mode de conduite économe en carburant**

Hello partitionnée véhicule signaux et données de diagnostic sont traitées en pipeline hello nommé « FuelEfficientDrivingPatternPipeline ». Ruche est utilisé toodetermine hello modèles, emplacement, véhicule, conditions de conduite et autres propriétés qui exposent le modèle conduite efficace de carburant.

![Mode de conduite économe en carburant](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Figure 20 - Workflow du mode de conduite économe en carburant*

***Requête Hive du mode de conduite économe en carburant***

Hello script Hive nommé « fuelefficientdriving.hql » est utilisé pour analyser le modèle de condition déterminant agressif se trouve dans le dossier « \demo\src\connectedcar\scripts » de hello téléchargé zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Il utilise combinaison de hello de position de vitesse de transmission du véhicule, l’état de pédales frein, vitesse et carburant de toodetect position pédales accélérateur comportement conduite efficace en fonction de l’accélération, frein, et accélérer les modèles. 

Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.

![Sortie FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Figure 21 – Sortie FuelEfficientDrivingPatternPipeline*

**Prédictions des rappels**

expérience d’apprentissage Hello est configuré et publié comme un service web dans le cadre du déploiement de solutions hello. lot Hello calcul du score du point de terminaison est exploitée dans ce flux de travail, mis à l’aide des activités de score par lot d’une fabrique de données et enregistré comme un service lié de fabrique de données.

![Point de terminaison Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Figure 22 – Point de terminaison Machine Learning enregistré comme service lié dans Data Factory*

Hello service lié inscrit est utilisé dans les données de salutation hello DetectAnomalyPipeline tooscore à l’aide du modèle de détection d’anomalie hello. 

![Activité de notation par lot de Machine Learning dans Data Factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Figure 23 – Activité de notation par lot d’Azure Machine Learning dans Data Factory* 

Il existe quelques étapes effectuées dans ce pipeline pour préparer les données afin qu’il peut être operationalized avec lot hello calcul du score du service web. 

![DetectAnomalyPipeline pour la prédiction des véhicules nécessitant des rappels](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Figure 24 – DetectAnomalyPipeline pour la prédiction des véhicules nécessitant des rappels* 

***Requête Hive de détection des anomalies***

Une fois que le calcul de score hello est terminée, une activité HDInsight est tooprocess utilisé et les données d’agrégation hello sont classées en tant que les anomalies par modèle hello avec un score de probabilité de 0,60 ou supérieure.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.

![Sortie DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Figure 25 – Sortie DetectAnomalyPipeline*

## <a name="publish"></a>Publier

### <a name="real-time-analysis"></a>Analyse en temps réel
Une des requêtes hello dans la tâche de flux de données Analytique hello publie la sortie des tooan événements hello instance de concentrateur d’événements. 

![Tâche de flux de données Analytique publie tooan sortie instance de concentrateur d’événements](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Figure 26 : tâche de flux de données Analytique publie la sortie de tooan instance de concentrateur d’événements*

![Instance de concentrateur d’événements de sortie de flux de données Analytique requête toopublish toohello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Figure 27 : instance de concentrateur d’événements de sortie de flux de données Analytique requête toopublish toohello*

Ce flux d’événements est consommé par hello que realtimedashboardapp inclus dans les solutions hello. Cette application utilise le service de service web de requête-réponse de Machine Learning hello pour calculer les scores en temps réel et publie hello données résultantes tooa Power BI dataset pour la consommation. 

### <a name="batch-analysis"></a>Analyse en mode batch
résultats de Hello du lot de hello et de traitement en temps réel sont publiées toohello des tables de base de données SQL Azure pour la consommation. Bonjour Azure SQL Server, base de données et les tables de hello sont créés automatiquement en tant que partie du script de configuration hello. 

![Résultats du traitement par lots Copier le flux de travail toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Figure 28 – résultats de la copie toodata mart workflow de traitement par lots*

![Tâche de flux de données Analytique publie toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Figure 29 : tâche de flux de données Analytique publie toodata mart*

![Configuration de l’entrepôt de données dans la tâche Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Figure 30 – Configuration de l’entrepôt de données dans la tâche Stream Analytics*

## <a name="consume"></a>Utiliser
Power BI offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives. 

Cliquez ici pour obtenir des instructions détaillées sur la configuration des rapports de Power BI hello et tableau de bord hello. tableau de bord Hello final ressemble à ceci :

![Tableau de bord Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Figure 31 - Tableau de bord Power BI*

## <a name="summary"></a>Résumé
Ce document contient une exploration détaillée de hello véhicule télémétrie Analytique Solution. Il présente un modèle d’architecture lambda pour une analyse en temps réel et par lots reposant sur des prédictions et des actions. Ce modèle s’applique tooa large éventail de cas d’usage qui requièrent chemin réactif (en temps réel) et analytique de chemin d’accès à froid (lot). 

