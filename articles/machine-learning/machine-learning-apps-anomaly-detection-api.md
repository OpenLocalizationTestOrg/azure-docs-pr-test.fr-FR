---
title: "aaaAzure API de détection d’anomalie Machine Learning | Documents Microsoft"
description: "L’API de détection des anomalies est un exemple d’API généré avec Microsoft Azure Machine Learning. Elle détecte des anomalies dans les données de séries chronologiques présentant des valeurs numériques qui sont réparties uniformément dans le temps."
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>API de détection des anomalies Machine Learning
## <a name="overview"></a>Vue d'ensemble
L’[API de détection des anomalies](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) est un exemple d’API généré avec Microsoft Azure Machine Learning. Elle détecte des anomalies dans les données de séries chronologiques présentant des valeurs numériques qui sont réparties uniformément dans le temps.

Cette API peut détecter hello les types de modèles anormaux dans les données de série chronologique suivants :

* **Tendances positives et négatives :**par exemple, pendant l’analyse de l’utilisation de la mémoire de l’infrastructure informatique, une tendance à la hausse peut être digne d’intérêt, car elle est susceptible d’être le signe d’une fuite de mémoire.
* **Modifications dans la plage dynamique de hello de valeurs**: par exemple, lors de l’analyse des exceptions hello levées par un service cloud, les modifications apportées à la plage dynamique de hello de valeurs peut indiquer une instabilité dans le contrôle d’intégrité hello du service de hello, et
* **Des pics se produisent et DIP**: par exemple, lors de l’analyse de nombre hello d’échecs de connexion dans un service ou le nombre d’extractions dans un site de commerce électronique, pics ou les adresses IP dynamiques peut indiquer un comportement anormal.

Ces détecteurs Machine Learning effectuent le suivi de tels changements de valeurs au fil du temps, signalant les changements en continu au sein de leurs valeurs en tant que résultats d’anomalies. Ils ne nécessitent pas de réglage du seuil ad hoc et leurs scores peuvent être des taux de toocontrol utilisé faux positifs. détection d’anomalie Hello API est utile dans plusieurs scénarios tels que le service d’analyse en effectuant le suivi des indicateurs de performance clés au fil du temps, l’utilisation de surveillance via les métriques, telles que le nombre de recherches, le nombre de clics, d’analyse des performances des compteurs de mémoire, processeur, fichier lit, etc. au fil du temps.

offre de détection d’anomalie Hello est fourni avec tooget outils utiles que vous avez démarré.

* Hello [application web](http://anomalydetection-aml.azurewebsites.net/) vous permet d’évaluer et de visualiser les résultats de hello de détection d’anomalie API sur vos données.

> [!NOTE]
> Essayez la **solution IT Anomaly Insights** basée sur [cette API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).
> 
> tooget cette solution de tooend fin déployé tooyour abonnement Azure <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **Démarrer ici >**</a>
> 
>

## <a name="api-deployment"></a>Déploiement de l’API
Bonjour toouse de commande API, vous devez le déployer tooyour abonnement Azure, où il sera hébergé comme un service web Azure Machine Learning.  Vous pouvez les spécifier cela via hello [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  Cette action déploie deux AzureML Web Services (et leurs ressources associées) tooyour abonnement Azure - un pour la détection d’anomalie avec détection de saisonnalité et que l’autre sans la détection de saisonnalité.  Une fois le déploiement de hello est terminé, vous serez toomanage en mesure de votre API à partir de hello [AzureML des services web](https://services.azureml.net/webservices/) page.  À partir de cette page, vous serez être en mesure de toofind les emplacements de votre point de terminaison, les clés API, ainsi qu’exemples de code pour appeler les API hello.  Des instructions plus détaillées sont disponibles [ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice).

## <a name="scaling-hello-api"></a>Mise à l’échelle hello API
Par défaut, votre déploiement dispose d’un plan de facturation gratuit de développement/test qui comprend 1 000 transactions par mois et 2 heures de calcul par mois.  Vous pouvez mettre à niveau tooanother plan conformément à vos besoins.  Détails sur la tarification de hello de plans différents sont disponibles [ici](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) sous « Tarification API Web de Production ».

## <a name="managing-aml-plans"></a>Gestion des plans AML 
Vous pouvez gérer votre plan de facturation [ici](https://services.azureml.net/plans/).  nom du plan Hello est basé sur le nom de groupe de ressources hello que vous avez choisi lors du déploiement d’API de hello, plus une chaîne qui est unique tooyour abonnement.  Obtenir des instructions sur la façon dont tooupgrade votre plan sont disponibles [ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) sous la section « Gestion des plans de facturation » de hello.

## <a name="api-definition"></a>Définition de l’API
Hello service web fournit une API basée sur REST sur HTTPS qui peuvent être utilisés de différentes façons, notamment un rôle web ou application mobile, R, Python, Excel, etc..  Vous envoyez votre service de toothis de données de série heure via un appel d’API REST, et elle s’exécute une combinaison des trois types d’anomalies hello, décrit ci-dessous.

## <a name="calling-hello-api"></a>Appel de l’API de hello
Bonjour toocall de commande API, vous devez clé API et emplacement de point de terminaison tooknow hello.  Ces deux éléments, ainsi que des exemples de code pour appeler les API de hello, sont disponibles à partir de hello [AzureML des services web](https://services.azureml.net/webservices/) page.  Parcourir les API toohello souhaité, puis cliquez sur hello « Consommer » onglet toofind les.  Notez que vous pouvez appeler des API hello en tant que Swagger API (c'est-à-dire avec un paramètre d’URL hello `format=swagger`) ou en tant qu’une API non Swagger (c'est-à-dire sans hello `format` paramètre d’URL).  exemple de code Hello utilise le format de Swagger hello.  Voici un exemple de demande et de réponse au format non-Swagger.  Ces exemples sont le point de terminaison toohello saisonnalité.  point de terminaison non-saisonnalité Hello est similaire.

### <a name="sample-request-body"></a>Exemple de corps de la demande
demande de Hello contient deux objets : `Inputs` et `GlobalParameters`.  Dans la requête d’exemple hello ci-dessous, certains paramètres sont envoyés explicitement tandis que d’autres ne le sont pas (faites défiler pour obtenir la liste complète des paramètres pour chaque point de terminaison).  Paramètres qui ne sont pas envoyées explicitement dans la demande de hello utilisent les valeurs de valeur par défaut hello répertoriés ci-dessous.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>Exemple de réponse
Notez que, dans hello toosee de commande `ColumnNames` champ, vous devez inclure `details=true` comme un paramètre d’URL dans votre demande.  Consultez les tableaux de hello ci-dessous pour hello signification de chacun de ces champs.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>API Score
Hello API de Score est utilisé pour la détection d’anomalie en cours d’exécution sur les données de série chronologique non saisonnières. Hello API s’exécute un nombre de détection d’anomalies dans les données de salutation et retourne leurs scores d’anomalies. figure Hello ci-dessous montre un exemple de détecter les anomalies qui hello que peut détecter les API de Score. Cette série chronologique inclut 2 changements de niveau distincts, ainsi que 3 pics. points de Hello rouge affichent les temps de hello à quels hello modification du niveau est détectée, tandis que les points de hello noir affichent les pics hello détecté.
![API Score][1]

### <a name="detectors"></a>Détecteurs
détection d’anomalie Hello API prend en charge les détecteurs 3 grandes catégories. Vous trouverez plus d’informations sur les paramètres d’entrée spécifiques et les sorties de chaque détecteur Bonjour tableau suivant.

| Catégorie de détecteurs | Détecteur | Description | Paramètres d’entrée | Sorties |
| --- | --- | --- | --- | --- |
| Détecteurs de pics |Détecteurs TSpike |Détecter des pics et des creux selon lointain hello sont des valeurs à partir de la première et la troisième quartile |*tspikedetector.Sensitivity :* prend entier dans la plage de hello par défaut de 1 à 10 : 3 ; Les valeurs élevées interceptera plus de valeurs extrêmes rendant ainsi moins sensibles |TSpike : valeurs binaires (1 si un pic/creux est détecté, 0 dans le cas contraire) |
| Détecteurs de pics | Détecteur ZSpike |Détecter des pics et des adresses IP dynamiques en fonction de décalage hello datapoints sont à leur moyenne |*zspikedetector.Sensitivity :* prendre de valeur entière dans la plage de hello par défaut de 1 à 10 : 3 ; Les valeurs élevées interceptera plus de valeurs extrêmes rendant moins sensibles |ZSpike : valeurs binaires (1 si un pic/creux est détecté, 0 dans le cas contraire) | |
| Détecteur de tendances lentes |Détecteur de tendances lentes |Détecter une tendance positive lente en fonction de la sensibilité du jeu hello |*trenddetector.Sensitivity :* seuil de score de détecteur (valeur par défaut : 3,25, 3,25 – 5 est une plage acceptable de tooselect à partir ; hello hello supérieur moins sensible) |tscore : nombre flottant représentant le résultat d’anomalies pour une tendance |
| Détecteurs de changements de niveau | Détecteur de changements de niveau bidirectionnels |Détecter une modification à la fois vers le haut et vers le bas niveau en fonction de la sensibilité du jeu hello |*bileveldetector.Sensitivity :* seuil de score de détecteur (valeur par défaut : 3,25, 3,25 – 5 est une plage acceptable de tooselect à partir ; hello hello supérieur moins sensible) |rscore : nombre flottant représentant le résultat d’anomalies pour un changement de niveau vers le haut et vers le bas | |

### <a name="parameters"></a>Paramètres
Des informations plus détaillées sur ces paramètres d’entrée sont répertoriées dans le tableau hello ci-dessous :

| Paramètres d’entrée | Description | Paramètre par défaut | Type | Plage valide | Plage suggérée |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |Historique (en nombre de points de données) utilisé pour le calcul du résultat d’anomalies |500 |integer |10-2000 |Dépend des séries chronologiques |
| detectors.spikesdips | Si toodetect uniquement des pics se produisent, les adresses IP dynamiques uniquement ou les deux |Les deux |enumerated |Les deux, pics, creux |Les deux |
| bileveldetector.sensitivity |Sensibilité du détecteur de changements de niveau bidirectionnels. |3.25 |double |Aucune |3.25-5 (plus la valeur est basse, plus la sensibilité est importante) |
| trenddetector.sensitivity |Sensibilité du détecteur de tendances positives |3.25 |double |Aucune |3.25-5 (plus la valeur est basse, plus la sensibilité est importante) |
| tspikedetector.sensitivity |Sensibilité du détecteur TSpike |3 |integer |1-10 |3-5 (plus la valeur est basse, plus la sensibilité est importante) |
| zspikedetector.sensitivity |Sensibilité du détecteur ZSpike |3 |integer |1-10 |3-5 (plus la valeur est basse, plus la sensibilité est importante) |
| postprocess.tailRows |Nombre de données les plus récentes hello points toobe conservé dans les résultats de sortie hello |0 |integer |0 (conserver tous les points de données), ou spécifiez le nombre de points tookeep dans les résultats |N/A |

### <a name="output"></a>Sortie
Hello API s’exécute tous les détecteurs sur vos données de série chronologique et retourne les scores d’anomalies et les indicateurs de pic binaire pour chaque point dans le temps. Hello ci-dessous répertorie les sorties à partir de l’API de hello. 

| outputs | Description |
| --- | --- |
| Time |Horodatages issus des données brutes ou des données agrégées (et/ou) imputées si l’imputation des données agrégées (et/ou) manquantes est appliquée. |
| Données |Valeurs issues des données brutes ou des données agrégées (et/ou) imputées si l’imputation des données agrégées (et/ou) manquantes est appliquée. |
| TSpike |Indicateur binaire tooindicate si un pic d’activité est détectée par le détecteur de TSpike |
| ZSpike |Indicateur binaire tooindicate si un pic d’activité est détectée par le détecteur de ZSpike |
| rpscore |Nombre flottant représentant le résultat d’anomalies pour un changement de niveau bidirectionnel |
| rpalert |valeur de 1/0 qui indique le niveau de bidirectionnel est changer d’anomalie basée sur la sensibilité d’entrée de hello |
| tscore |Nombre flottant représentant le résultat d’anomalies pour une tendance positive |
| talert |valeur de 1/0 indiquant qu’est une anomalie tendance positive en fonction de la sensibilité d’entrée de hello |

## <a name="scorewithseasonality-api"></a>API ScoreWithSeasonality
Hello ScoreWithSeasonality API est utilisée pour l’exécution de la détection d’anomalies de série chronologique qui ont des modèles saisonnières. Cette API méthode est utile toodetect les écarts dans les modèles saisonnières.  
Hello figure suivante montre un exemple d’anomalies détecté dans une série chronologique saisonnières. MTS Hello possède un pic (point noir 1er hello), deux creux (point de noir 2e hello et une des extrémités hello) et une modification du niveau (point rouge). Notez que les deux hello dip au milieu de hello de MTS hello et modification du niveau de hello sont uniquement peuvent être distinguées après saisonnières sont supprimés de la série de hello.
![API Saisonnalité][2]

### <a name="detectors"></a>Détecteurs
détecteurs Hello dans le point de terminaison de saisonnalité hello sont similaires toohello ceux dans le point de terminaison non-saisonnalité hello, mais avec des noms de paramètres légèrement différents (répertoriés ci-après).

### <a name="parameters"></a>Paramètres

Des informations plus détaillées sur ces paramètres d’entrée sont répertoriées dans le tableau hello ci-dessous :

| Paramètres d’entrée | Description | Paramètre par défaut | Type | Plage valide | Plage suggérée |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Intervalle d’agrégation en secondes pour l’agrégation de séries chronologiques d’entrée |0 (aucune agrégation n’est effectuée) |integer |0 : ignorer l’agrégation, > 0 autrement |jour de too1 de 5 minutes, dépendant de la série chronologique |
| preprocess.aggregationFunc |Fonction utilisée pour agréger les données en hello spécifié AggregationInterval |mean |enumerated |mean, sum, length |N/A |
| preprocess.replaceMissing |Les valeurs utilisées tooimpute des données manquantes |lkv (dernière valeur connue) |enumerated |zero, lkv, mean |N/A |
| detectors.historyWindow |Historique (en nombre de points de données) utilisé pour le calcul du résultat d’anomalies |500 |integer |10-2000 |Dépend des séries chronologiques |
| detectors.spikesdips | Si toodetect uniquement des pics se produisent, les adresses IP dynamiques uniquement ou les deux |Les deux |enumerated |Les deux, pics, creux |Les deux |
| bileveldetector.sensitivity |Sensibilité du détecteur de changements de niveau bidirectionnels. |3.25 |double |Aucune |3.25-5 (plus la valeur est basse, plus la sensibilité est importante) |
| postrenddetector.sensitivity |Sensibilité du détecteur de tendances positives |3.25 |double |Aucune |3.25-5 (plus la valeur est basse, plus la sensibilité est importante) |
| negtrenddetector.sensitivity |Sensibilité du détecteur de tendances négatives. |3.25 |double |Aucune |3.25-5 (plus la valeur est basse, plus la sensibilité est importante) |
| tspikedetector.sensitivity |Sensibilité du détecteur TSpike |3 |integer |1-10 |3-5 (plus la valeur est basse, plus la sensibilité est importante) |
| zspikedetector.sensitivity |Sensibilité du détecteur ZSpike |3 |integer |1-10 |3-5 (plus la valeur est basse, plus la sensibilité est importante) |
| seasonality.enable |Si l’analyse saisonnalité est toobe effectuée |true |booléenne |true, false |Dépend des séries chronologiques |
| seasonality.numSeasonality |Nombre maximal de toobe cycles périodiques détecté |1 |integer |1, 2 |1-2 |
| seasonality.transform |Suppression des composantes de tendances (et) saisonnières avant l’exécution de la détection des anomalies |deseason |enumerated |none, deseason, deseasontrend |N/A |
| postprocess.tailRows |Nombre de données les plus récentes hello points toobe conservé dans les résultats de sortie hello |0 |integer |0 (conserver tous les points de données), ou spécifiez le nombre de points tookeep dans les résultats |N/A |

### <a name="output"></a>Sortie
Hello API s’exécute tous les détecteurs sur vos données de série chronologique et retourne les scores d’anomalies et les indicateurs de pic binaire pour chaque point dans le temps. Hello ci-dessous répertorie les sorties à partir de l’API de hello. 

| outputs | Description |
| --- | --- |
| Time |Horodatages issus des données brutes ou des données agrégées (et/ou) imputées si l’imputation des données agrégées (et/ou) manquantes est appliquée. |
| OriginalData |Valeurs issues des données brutes ou des données agrégées (et/ou) imputées si l’imputation des données agrégées (et/ou) manquantes est appliquée. |
| ProcessedData |Un des éléments suivants de hello : <ul><li>série chronologique ajustée de façon saisonnière si un caractère saisonnier important a été détectée et si l’option deseason est sélectionnée ;</li><li>série chronologique redressée et ajustée de façon saisonnière si un caractère saisonnier important a été détectée et si l’option deseasontrend est sélectionnée ;</li><li>dans le cas contraire, cela est hello identique OriginalData</li> |
| TSpike |Indicateur binaire tooindicate si un pic d’activité est détectée par le détecteur de TSpike |
| ZSpike |Indicateur binaire tooindicate si un pic d’activité est détectée par le détecteur de ZSpike |
| BiLevelChangeScore |Nombre flottant représentant le résultat d’anomalies pour un changement de niveau |
| BiLevelChangeAlert |1/0 valeur indiquant qu’est une anomalie de changement de niveau en fonction de la sensibilité d’entrée de hello |
| PosTrendScore |Nombre flottant représentant le résultat d’anomalies pour une tendance positive |
| PosTrendAlert |valeur de 1/0 indiquant qu’est une anomalie tendance positive en fonction de la sensibilité d’entrée de hello |
| NegTrendScore |Nombre flottant représentant le résultat d’anomalies pour une tendance négative |
| NegTrendAlert |valeur de 1/0 indiquant qu’est une anomalie tendance négative en fonction de la sensibilité d’entrée de hello |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

