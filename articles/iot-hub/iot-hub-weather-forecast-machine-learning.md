---
title: "Prévision météo utilisant les données Microsoft Machine Learning de votre IoT Hub | Microsoft Docs"
description: "Utilisez Azure Machine Learning pour prédire le risque de pluie sur la base des données de température et d’humidité que votre IoT Hub collecte à partir d’un capteur."
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
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="cbbeb-104">Prévision météo utilisant les données de capteur de votre IoT Hub dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cbbeb-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="cbbeb-106">L’apprentissage automatique (Machine Learning) utilise des ordinateurs pour exécuter des modèles prédictifs qui apprennent à partir de données existantes afin de prévoir les tendances, résultats et comportements futurs.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="cbbeb-107">Azure Machine Learning est un service d’analyse prédictive sur le cloud qui permet de créer et de déployer rapidement des modèles prédictifs sous forme de solutions d’analyse.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cbbeb-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="cbbeb-108">What you learn</span></span>

<span data-ttu-id="cbbeb-109">Vous apprenez à utiliser Azure Machine Learning pour effectuer des prévisions (de chances de pluie) en utilisant les données de température et d’humidité de votre Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="cbbeb-110">Les chances de sortie sont la sortie d’un modèle de prévision météo préparé.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="cbbeb-111">Le modèle est basé sur des données historiques pour prévoir les chances de pluie en fonction de la température et de l’humidité.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="cbbeb-112">Procédure</span><span class="sxs-lookup"><span data-stu-id="cbbeb-112">What you do</span></span>

- <span data-ttu-id="cbbeb-113">Déployez le modèle de prévision météo comme un service web.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="cbbeb-114">Préparez votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="cbbeb-115">Créez un travail Stream Analytics et configurez-le pour :</span><span class="sxs-lookup"><span data-stu-id="cbbeb-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="cbbeb-116">Lire les données de température et d’humidité en temps réel à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="cbbeb-117">Appelez le service web pour obtenir les chances de pluie.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="cbbeb-118">Enregistrer les résultats dans un stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="cbbeb-119">Utilisez Microsoft Azure Storage Explorer pour afficher les prévisions météorologiques.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cbbeb-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="cbbeb-120">What you need</span></span>

- <span data-ttu-id="cbbeb-121">Le didacticiel [Configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé, qui traite des exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbbeb-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="cbbeb-122">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="cbbeb-123">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="cbbeb-124">Une application cliente qui envoie des messages à votre instance Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="cbbeb-125">Un compte Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="cbbeb-126">([Essayez Machine Learning Studio gratuitement](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="cbbeb-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="cbbeb-127">Déployer le modèle de prévision météo comme un service web</span><span class="sxs-lookup"><span data-stu-id="cbbeb-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="cbbeb-128">Accédez à la [page de modèle de prévision météo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="cbbeb-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="cbbeb-129">Cliquez sur **Ouvrir dans Studio** dans Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="cbbeb-130">![Ouvrez la page de modèle de prévision météo dans la galerie Cortana Intelligence](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="cbbeb-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="cbbeb-131">Cliquez sur **Exécuter** pour valider les étapes du modèle.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="cbbeb-132">Cette étape peut prendre 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="cbbeb-133">![Ouverture du modèle de prévision météorologique dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="cbbeb-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="cbbeb-134">Cliquez sur **CONFIGURER LE SERVICE WEB** > **Service web prédictif**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="cbbeb-135">![Déploiement du modèle de prévision météorologique dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="cbbeb-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="cbbeb-136">Dans le diagramme, faites glisser le module **Entrée du service web** près du module **Modèle de score**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="cbbeb-137">Connectez le module **Entrée du service web** au module **Modèle de score**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="cbbeb-138">![Connexion de deux modules dans Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="cbbeb-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="cbbeb-139">Cliquez sur **EXÉCUTER** pour valider les étapes du modèle.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="cbbeb-140">Cliquez sur **DÉPLOYER LE SERVICE WEB** pour déployer le modèle en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="cbbeb-141">Sur le tableau de bord du modèle, téléchargez le classeur **Excel 2010 ou version antérieure**  pour **DEMANDE/RÉPONSE**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="cbbeb-142">Assurez-vous de télécharger le classeur **Excel 2010 ou version antérieure** même si vous exécutez une version ultérieure d’Excel sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Téléchargement du classeur Excel pour le point de terminaison DEMANDE/RÉPONSE](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="cbbeb-144">Ouvrez le classeur Excel, notez **l’URL DU SERVICE WEB** et la **CLÉ D’ACCÈS**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="cbbeb-145">Créer, configurer et exécuter un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbbeb-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="cbbeb-146">Création d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbbeb-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="cbbeb-147">Dans le [portail Azure](https://ms.portal.azure.com/), cliquez sur **Nouveau** > **Internet des objets** > **Travail Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="cbbeb-148">Saisissez les informations ci-après concernant le travail.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="cbbeb-149">**Nom du travail** : nom du travail.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="cbbeb-150">Le nom doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-150">The name must be globally unique.</span></span>

   <span data-ttu-id="cbbeb-151">**Groupe de ressources** : utilisez le groupe de ressources que votre instance IoT Hub exploite.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="cbbeb-152">**Emplacement** : utilisez le même emplacement que votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="cbbeb-153">**Épingler au tableau de bord** : cochez cette option pour pouvoir accéder facilement à votre instance IoT Hub à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Créer un travail Stream Analytics dans Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="cbbeb-155">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="cbbeb-156">Ajouter une entrée au travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbbeb-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="cbbeb-157">Ouvrez le travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="cbbeb-158">Sous **Topologie du travail**, cliquez sur **Entrées**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="cbbeb-159">Dans le volet **Entrées**, cliquez sur **Ajouter**, puis saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbbeb-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="cbbeb-160">**Alias d’entrée** : alias unique de l’entrée.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="cbbeb-161">**Source** : sélectionnez **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="cbbeb-162">**Groupe de consommateurs** : sélectionnez le groupe de consommateurs que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Ajouter une entrée à un travail Stream Analytics dans Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="cbbeb-164">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="cbbeb-165">Ajouter une sortie au travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbbeb-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="cbbeb-166">Sous **Topologie du travail**, cliquez sur **Sorties**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="cbbeb-167">Dans le volet **Sorties**, cliquez sur **Ajouter**, puis saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbbeb-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="cbbeb-168">**Alias de sortie** : alias unique de la sortie.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="cbbeb-169">**Sink** : sélectionnez **Stockage d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="cbbeb-170">**Compte de stockage** : Le compte de stockage pour votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="cbbeb-171">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="cbbeb-172">**Conteneur** : le conteneur dans lequel l’objet blob est enregistré.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="cbbeb-173">Vous pouvez créer un conteneur ou utiliser un conteneur existant.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="cbbeb-174">**Format de sérialisation de l’événement** : Sélectionnez **CSV**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Ajouter une sortie à un travail Stream Analytics dans Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="cbbeb-176">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="cbbeb-177">Ajouter une fonction au travail Stream Analytics pour appeler le service web que vous avez déployé</span><span class="sxs-lookup"><span data-stu-id="cbbeb-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="cbbeb-178">Sous **Topologie du travail**, cliquez sur **Fonctions** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="cbbeb-179">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbbeb-179">Enter the following information:</span></span>

   <span data-ttu-id="cbbeb-180">**Alias de la fonction** : entrez `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="cbbeb-181">**Type de fonction** : sélectionnez **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="cbbeb-182">**Option d’importation** : sélectionnez **Importer à partir d’un autre abonnement**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="cbbeb-183">**URL** : entrez l’URL DU SERVICE WEB que vous avez notée à partir du classeur Excel.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="cbbeb-184">**Clé** : entrez la CLÉ D’ACCÈS que vous avez notée à partir du classeur Excel.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Ajouter une requête à un travail Stream Analytics dans Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="cbbeb-186">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="cbbeb-187">Configurer la requête du travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbbeb-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="cbbeb-188">Sous **Topologie du travail**, cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="cbbeb-189">Remplacez le code existant par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="cbbeb-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="cbbeb-190">Remplacez `[YourInputAlias]` par l’alias d’entrée du travail.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="cbbeb-191">Remplacez `[YourOutputAlias]` par l’alias de sortie du travail.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="cbbeb-192">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="cbbeb-193">Exécuter la tâche Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cbbeb-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="cbbeb-194">Dans le travail Stream Analytics, cliquez sur **Démarrer** > **Maintenant** > **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="cbbeb-195">Une fois le travail lancé, l’état correspondant passe de **Arrêté** à **Exécution**.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Exécuter la tâche Stream Analytics](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="cbbeb-197">Utiliser Microsoft Azure Storage Explorer pour afficher les prévisions météorologiques</span><span class="sxs-lookup"><span data-stu-id="cbbeb-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="cbbeb-198">Exécutez l’application cliente pour commencer la collecte et l’envoi de données de température et d’humidité à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="cbbeb-199">Pour chaque message que votre IoT Hub reçoit, le travail Stream Analytics appelle le service web de prévision météorologique pour produire les chances de pluie.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="cbbeb-200">Le résultat est ensuite enregistré dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="cbbeb-201">Azure Storage Explorer est un outil que vous pouvez utiliser pour afficher le résultat.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="cbbeb-202">[Téléchargez et installez Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="cbbeb-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="cbbeb-203">Ouvrez l’Explorateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="cbbeb-204">Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="cbbeb-205">Sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-205">Select your subscription.</span></span>
1. <span data-ttu-id="cbbeb-206">Cliquez sur votre abonnement **Comptes de stockage** > votre compte de stockage > **Conteneurs d’objets blob** > Votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="cbbeb-207">Ouvrez un fichier .csv pour voir le résultat.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="cbbeb-208">La dernière colonne enregistre les chances de pluie.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-208">The last column records the chance of rain.</span></span>

   ![Obtenir des résultats de prévisions météo avec Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="cbbeb-210">Résumé</span><span class="sxs-lookup"><span data-stu-id="cbbeb-210">Summary</span></span>

<span data-ttu-id="cbbeb-211">Vous avez correctement utilisé Azure Machine Learning pour produire le risque de pluie sur la base des données de température et d’humidité que votre IoT Hub reçoit.</span><span class="sxs-lookup"><span data-stu-id="cbbeb-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]