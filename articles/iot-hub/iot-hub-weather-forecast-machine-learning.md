---
title: "aaaWeather de prévision à l’aide d’Azure Machine Learning avec des données à partir de IoT Hub | Documents Microsoft"
description: "Utilisez Azure Machine Learning toopredict hello chance de train selon humidité et de température de hello votre hub IoT collecte à partir d’un capteur de données."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Prévisions météo avec Machine Learning"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Prévisions météorologiques à l’aide des données de capteur hello à partir de votre hub IoT dans Azure Machine Learning

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Apprentissage est une technique de science des données qui aide les ordinateurs à partir des tendances, les résultats et les comportements futurs de tooforecast des données existantes. Azure Machine Learning est un service cloud prédictive analytique qui rend possible tooquickly créer et déployer des modèles prédictifs en tant que solutions d’analytique.

## <a name="what-you-learn"></a>Contenu

Vous allez apprendre comment à l’aide de toouse Azure Machine Learning toodo météo (risque de train) hello des données de température et humidité votre concentrateur Azure IoT. risque de Hello de train est sortie hello d’un modèle de prévision météo préparée. modèle de Hello est basé sur chance de tooforecast des données historiques de train en fonction de la température et humidité.

## <a name="what-you-do"></a>Procédure

- Déployer le modèle de prévision météo hello comme un service web.
- Préparez votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.
- Créer une tâche de flux de données Analytique et configurer la tâche hello pour :
  - Lire les données de température et d’humidité en temps réel à partir de votre IoT Hub.
  - Appelez la chance de hello web service tooget hello train.
  - Enregistrez le stockage d’objets blob Azure hello résultat tooan.
- Utilisez Microsoft Azure Storage Explorer tooview hello météo.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :
  - Un abonnement Azure actif.
  - Une instance Azure IoT Hub associée à votre abonnement.
  - Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.
- Un compte Azure Machine Learning Studio. ([Essayez Machine Learning Studio gratuitement](https://studio.azureml.net/)).

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Déployer le modèle de prévision météo hello comme un service web

1. Accédez toohello [page modèle de prévision météo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Cliquez sur **Ouvrir dans Studio** dans Microsoft Azure Machine Learning Studio.
   ![Page de modèle de prédiction de météo hello ouvrir dans la galerie de Cortana Intelligence](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Cliquez sur **exécuter** toovalidate hello les étapes dans le modèle de hello. Cette étape peut prendre 2 minutes toocomplete.
   ![Modèle de prévision météo hello ouvert dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Cliquez sur **CONFIGURER LE SERVICE WEB** > **Service web prédictif**.
   ![Déployer le modèle de prévision météo hello dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Dans le diagramme de hello, faites glisser hello **Web service entrée** module à hello **Score Model** module.
1. Se connecter hello **Web service entrée** module toohello **Score Model** module.
   ![Connexion de deux modules dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Cliquez sur **exécuter** toovalidate hello les étapes dans le modèle de hello.
1. Cliquez sur **déployer le SERVICE WEB** modèle de hello toodeploy comme un service web.
1. Tableau de bord hello du modèle de hello, télécharger hello **Excel 2010 ou classeur antérieur** pour **demande/réponse**.

   > [!Note]
   > Assurez-vous que vous téléchargez hello **Excel 2010 ou classeur antérieur** même si vous exécutez une version ultérieure de Microsoft Excel sur votre ordinateur.

   ![Télécharger hello Excel pour le point de terminaison de réponse demande hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Ouvrez le classeur Excel de hello, prenez note de hello **URL du SERVICE WEB** et **clé d’accès**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Créer, configurer et exécuter un travail Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Création d’un travail Stream Analytics

1. Bonjour [portail Azure](https://ms.portal.azure.com/), cliquez sur **nouveau** > **Internet of Things** > **tâche de flux de données Analytique**.
1. Entrez hello informations pour le travail de hello suivantes.

   **Nom de la tâche**: nom hello du travail de hello. nom de Hello doit être globalement unique.

   **Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.

   **Emplacement**: utilisez hello même emplacement que votre groupe de ressources.

   **Code confidentiel toodashboard**: Activez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.

   ![Créer un travail Stream Analytics dans Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Cliquez sur **Créer**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Ajouter une tâche de flux de données Analytique toohello d’entrée

1. Tâche de flux de données Analytique hello ouvert.
1. Sous **Topologie du travail**, cliquez sur **Entrées**.
1. Bonjour **entrées** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :

   **Alias d’entrée**: alias unique de hello pour l’entrée de hello.

   **Source** : sélectionnez **IoT Hub**.

   **Groupe de consommateurs**: groupe de consommateurs hello sélectionnez vous avez créé.

   ![Ajouter une tâche de flux de données Analytique toohello d’entrée dans Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Cliquez sur **Créer**.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Ajouter une tâche de flux de données Analytique toohello sortie

1. Sous **Topologie du travail**, cliquez sur **Sorties**.
1. Bonjour **sorties** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :

   **Alias de sortie**: alias unique de hello pour la sortie de hello.

   **Sink** : sélectionnez **Stockage d’objets blob**.

   **Compte de stockage**: hello compte de stockage pour votre stockage d’objets blob. Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.

   **Conteneur**: conteneur hello dans lequel l’objet blob de hello est enregistré. Vous pouvez créer un conteneur ou utiliser un conteneur existant.

   **Format de sérialisation de l’événement** : Sélectionnez **CSV**.

   ![Ajouter une tâche de flux de données Analytique sortie toohello dans Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Cliquez sur **Créer**.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Ajouter un service web Analytique de flux travail toocall hello vous avez déployé de toohello (fonction)

1. Sous **Topologie du travail**, cliquez sur **Fonctions** > **Ajouter**.
1. Entrez hello informations suivantes :

   **Alias de la fonction** : entrez `machinelearning`.

   **Type de fonction** : sélectionnez **Azure ML**.

   **Option d’importation** : sélectionnez **Importer à partir d’un autre abonnement**.

   **URL**: entrez hello URL du SERVICE WEB que vous avez notée vers le bas à partir du classeur Excel de hello.

   **Clé**: entrez hello clé d’accès que vous avez pris note vers le bas à partir du classeur Excel de hello.

   ![Ajouter une tâche de flux de données Analytique toohello (fonction) dans Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Cliquez sur **Créer**.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurer la requête hello de tâche de flux de données Analytique hello

1. Sous **Topologie du travail**, cliquez sur **Requête**.
1. Remplacez le code existant hello hello suivant de code :

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Remplacez `[YourInputAlias]` avec alias hello d’entrée de tâche de hello.

   Remplacez `[YourOutputAlias]` avec l’alias de sortie hello du travail de hello.

1. Cliquez sur **Enregistrer**.

### <a name="run-hello-stream-analytics-job"></a>Exécuter la tâche de flux de données Analytique hello

Dans la tâche de flux de données Analytique hello, cliquez sur **Démarrer** > **maintenant** > **Démarrer**. Une fois le travail de hello démarre avec succès, état de la tâche hello passe de **arrêté** trop**en cours d’exécution**.

![Exécuter la tâche de flux de données Analytique hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Utiliser Microsoft Azure Storage Explorer tooview hello météo

Exécutez toostart de hello d’application de client collecte et l’envoi de température et humidité données tooyour IoT hub. Pour chaque message qui reçoit de votre hub IoT, la tâche de flux de données Analytique hello appelle chance hello hello prévisions météorologiques web service tooproduce de train. résultat de Hello est ensuite enregistré stockage d’objets blob Azure tooyour. Explorateur de stockage Azure est un outil que vous pouvez utiliser le résultat de hello tooview.

1. [Téléchargez et installez Microsoft Azure Storage Explorer](http://storageexplorer.com/).
1. Ouvrez l’Explorateur de stockage Azure.
1. Se connecter tooyour compte Azure.
1. Sélectionnez votre abonnement.
1. Cliquez sur votre abonnement **Comptes de stockage** > votre compte de stockage > **Conteneurs d’objets blob** > Votre conteneur.
1. Ouvrir un fichier .csv toosee le résultat hello. derniers enregistrements de colonne Hello hello risque de train.

   ![Obtenir des résultats de prévisions météo avec Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Résumé

Vous avez utilisé avec succès chance de hello Azure Machine Learning tooproduce de train en fonction des données de température et humidité hello qui reçoit de votre hub IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]