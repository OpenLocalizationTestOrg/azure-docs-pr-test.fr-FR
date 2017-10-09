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
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="26bab-104">Prévisions météorologiques à l’aide des données de capteur hello à partir de votre hub IoT dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="26bab-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="26bab-106">Apprentissage est une technique de science des données qui aide les ordinateurs à partir des tendances, les résultats et les comportements futurs de tooforecast des données existantes.</span><span class="sxs-lookup"><span data-stu-id="26bab-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="26bab-107">Azure Machine Learning est un service cloud prédictive analytique qui rend possible tooquickly créer et déployer des modèles prédictifs en tant que solutions d’analytique.</span><span class="sxs-lookup"><span data-stu-id="26bab-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="26bab-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="26bab-108">What you learn</span></span>

<span data-ttu-id="26bab-109">Vous allez apprendre comment à l’aide de toouse Azure Machine Learning toodo météo (risque de train) hello des données de température et humidité votre concentrateur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="26bab-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="26bab-110">risque de Hello de train est sortie hello d’un modèle de prévision météo préparée.</span><span class="sxs-lookup"><span data-stu-id="26bab-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="26bab-111">modèle de Hello est basé sur chance de tooforecast des données historiques de train en fonction de la température et humidité.</span><span class="sxs-lookup"><span data-stu-id="26bab-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="26bab-112">Procédure</span><span class="sxs-lookup"><span data-stu-id="26bab-112">What you do</span></span>

- <span data-ttu-id="26bab-113">Déployer le modèle de prévision météo hello comme un service web.</span><span class="sxs-lookup"><span data-stu-id="26bab-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="26bab-114">Préparez votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="26bab-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="26bab-115">Créer une tâche de flux de données Analytique et configurer la tâche hello pour :</span><span class="sxs-lookup"><span data-stu-id="26bab-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="26bab-116">Lire les données de température et d’humidité en temps réel à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="26bab-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="26bab-117">Appelez la chance de hello web service tooget hello train.</span><span class="sxs-lookup"><span data-stu-id="26bab-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="26bab-118">Enregistrez le stockage d’objets blob Azure hello résultat tooan.</span><span class="sxs-lookup"><span data-stu-id="26bab-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="26bab-119">Utilisez Microsoft Azure Storage Explorer tooview hello météo.</span><span class="sxs-lookup"><span data-stu-id="26bab-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="26bab-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="26bab-120">What you need</span></span>

- <span data-ttu-id="26bab-121">Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="26bab-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="26bab-122">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="26bab-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="26bab-123">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="26bab-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="26bab-124">Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="26bab-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="26bab-125">Un compte Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="26bab-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="26bab-126">([Essayez Machine Learning Studio gratuitement](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="26bab-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="26bab-127">Déployer le modèle de prévision météo hello comme un service web</span><span class="sxs-lookup"><span data-stu-id="26bab-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="26bab-128">Accédez toohello [page modèle de prévision météo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="26bab-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="26bab-129">Cliquez sur **Ouvrir dans Studio** dans Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="26bab-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="26bab-130">![Page de modèle de prédiction de météo hello ouvrir dans la galerie de Cortana Intelligence](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="26bab-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="26bab-131">Cliquez sur **exécuter** toovalidate hello les étapes dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="26bab-132">Cette étape peut prendre 2 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="26bab-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="26bab-133">![Modèle de prévision météo hello ouvert dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="26bab-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="26bab-134">Cliquez sur **CONFIGURER LE SERVICE WEB** > **Service web prédictif**.</span><span class="sxs-lookup"><span data-stu-id="26bab-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="26bab-135">![Déployer le modèle de prévision météo hello dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="26bab-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="26bab-136">Dans le diagramme de hello, faites glisser hello **Web service entrée** module à hello **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="26bab-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="26bab-137">Se connecter hello **Web service entrée** module toohello **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="26bab-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="26bab-138">![Connexion de deux modules dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="26bab-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="26bab-139">Cliquez sur **exécuter** toovalidate hello les étapes dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="26bab-140">Cliquez sur **déployer le SERVICE WEB** modèle de hello toodeploy comme un service web.</span><span class="sxs-lookup"><span data-stu-id="26bab-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="26bab-141">Tableau de bord hello du modèle de hello, télécharger hello **Excel 2010 ou classeur antérieur** pour **demande/réponse**.</span><span class="sxs-lookup"><span data-stu-id="26bab-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="26bab-142">Assurez-vous que vous téléchargez hello **Excel 2010 ou classeur antérieur** même si vous exécutez une version ultérieure de Microsoft Excel sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="26bab-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Télécharger hello Excel pour le point de terminaison de réponse demande hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="26bab-144">Ouvrez le classeur Excel de hello, prenez note de hello **URL du SERVICE WEB** et **clé d’accès**.</span><span class="sxs-lookup"><span data-stu-id="26bab-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="26bab-145">Créer, configurer et exécuter un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26bab-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="26bab-146">Création d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26bab-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="26bab-147">Bonjour [portail Azure](https://ms.portal.azure.com/), cliquez sur **nouveau** > **Internet of Things** > **tâche de flux de données Analytique**.</span><span class="sxs-lookup"><span data-stu-id="26bab-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="26bab-148">Entrez hello informations pour le travail de hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="26bab-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="26bab-149">**Nom de la tâche**: nom hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="26bab-150">nom de Hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="26bab-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="26bab-151">**Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="26bab-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="26bab-152">**Emplacement**: utilisez hello même emplacement que votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="26bab-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="26bab-153">**Code confidentiel toodashboard**: Activez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Créer un travail Stream Analytics dans Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="26bab-155">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26bab-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="26bab-156">Ajouter une tâche de flux de données Analytique toohello d’entrée</span><span class="sxs-lookup"><span data-stu-id="26bab-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="26bab-157">Tâche de flux de données Analytique hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="26bab-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="26bab-158">Sous **Topologie du travail**, cliquez sur **Entrées**.</span><span class="sxs-lookup"><span data-stu-id="26bab-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="26bab-159">Bonjour **entrées** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="26bab-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="26bab-160">**Alias d’entrée**: alias unique de hello pour l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="26bab-161">**Source** : sélectionnez **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="26bab-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="26bab-162">**Groupe de consommateurs**: groupe de consommateurs hello sélectionnez vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="26bab-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Ajouter une tâche de flux de données Analytique toohello d’entrée dans Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="26bab-164">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26bab-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="26bab-165">Ajouter une tâche de flux de données Analytique toohello sortie</span><span class="sxs-lookup"><span data-stu-id="26bab-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="26bab-166">Sous **Topologie du travail**, cliquez sur **Sorties**.</span><span class="sxs-lookup"><span data-stu-id="26bab-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="26bab-167">Bonjour **sorties** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="26bab-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="26bab-168">**Alias de sortie**: alias unique de hello pour la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="26bab-169">**Sink** : sélectionnez **Stockage d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="26bab-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="26bab-170">**Compte de stockage**: hello compte de stockage pour votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="26bab-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="26bab-171">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="26bab-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="26bab-172">**Conteneur**: conteneur hello dans lequel l’objet blob de hello est enregistré.</span><span class="sxs-lookup"><span data-stu-id="26bab-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="26bab-173">Vous pouvez créer un conteneur ou utiliser un conteneur existant.</span><span class="sxs-lookup"><span data-stu-id="26bab-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="26bab-174">**Format de sérialisation de l’événement** : Sélectionnez **CSV**.</span><span class="sxs-lookup"><span data-stu-id="26bab-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Ajouter une tâche de flux de données Analytique sortie toohello dans Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="26bab-176">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26bab-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="26bab-177">Ajouter un service web Analytique de flux travail toocall hello vous avez déployé de toohello (fonction)</span><span class="sxs-lookup"><span data-stu-id="26bab-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="26bab-178">Sous **Topologie du travail**, cliquez sur **Fonctions** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="26bab-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="26bab-179">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="26bab-179">Enter hello following information:</span></span>

   <span data-ttu-id="26bab-180">**Alias de la fonction** : entrez `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="26bab-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="26bab-181">**Type de fonction** : sélectionnez **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="26bab-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="26bab-182">**Option d’importation** : sélectionnez **Importer à partir d’un autre abonnement**.</span><span class="sxs-lookup"><span data-stu-id="26bab-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="26bab-183">**URL**: entrez hello URL du SERVICE WEB que vous avez notée vers le bas à partir du classeur Excel de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="26bab-184">**Clé**: entrez hello clé d’accès que vous avez pris note vers le bas à partir du classeur Excel de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Ajouter une tâche de flux de données Analytique toohello (fonction) dans Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="26bab-186">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26bab-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="26bab-187">Configurer la requête hello de tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="26bab-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="26bab-188">Sous **Topologie du travail**, cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="26bab-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="26bab-189">Remplacez le code existant hello hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="26bab-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="26bab-190">Remplacez `[YourInputAlias]` avec alias hello d’entrée de tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="26bab-191">Remplacez `[YourOutputAlias]` avec l’alias de sortie hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="26bab-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="26bab-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="26bab-193">Exécuter la tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="26bab-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="26bab-194">Dans la tâche de flux de données Analytique hello, cliquez sur **Démarrer** > **maintenant** > **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="26bab-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="26bab-195">Une fois le travail de hello démarre avec succès, état de la tâche hello passe de **arrêté** trop**en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="26bab-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Exécuter la tâche de flux de données Analytique hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="26bab-197">Utiliser Microsoft Azure Storage Explorer tooview hello météo</span><span class="sxs-lookup"><span data-stu-id="26bab-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="26bab-198">Exécutez toostart de hello d’application de client collecte et l’envoi de température et humidité données tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="26bab-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="26bab-199">Pour chaque message qui reçoit de votre hub IoT, la tâche de flux de données Analytique hello appelle chance hello hello prévisions météorologiques web service tooproduce de train.</span><span class="sxs-lookup"><span data-stu-id="26bab-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="26bab-200">résultat de Hello est ensuite enregistré stockage d’objets blob Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="26bab-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="26bab-201">Explorateur de stockage Azure est un outil que vous pouvez utiliser le résultat de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="26bab-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="26bab-202">[Téléchargez et installez Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="26bab-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="26bab-203">Ouvrez l’Explorateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="26bab-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="26bab-204">Se connecter tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="26bab-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="26bab-205">Sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="26bab-205">Select your subscription.</span></span>
1. <span data-ttu-id="26bab-206">Cliquez sur votre abonnement **Comptes de stockage** > votre compte de stockage > **Conteneurs d’objets blob** > Votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="26bab-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="26bab-207">Ouvrir un fichier .csv toosee le résultat hello.</span><span class="sxs-lookup"><span data-stu-id="26bab-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="26bab-208">derniers enregistrements de colonne Hello hello risque de train.</span><span class="sxs-lookup"><span data-stu-id="26bab-208">hello last column records hello chance of rain.</span></span>

   ![Obtenir des résultats de prévisions météo avec Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="26bab-210">Résumé</span><span class="sxs-lookup"><span data-stu-id="26bab-210">Summary</span></span>

<span data-ttu-id="26bab-211">Vous avez utilisé avec succès chance de hello Azure Machine Learning tooproduce de train en fonction des données de température et humidité hello qui reçoit de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="26bab-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]