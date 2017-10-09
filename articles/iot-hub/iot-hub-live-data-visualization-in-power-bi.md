---
title: "temps d’aaaReal visualisation des données de capteur à partir d’Azure IoT Hub – Power BI | Documents Microsoft"
description: "Utilisez les données de température et humidité de toovisualize Power BI qui sont collectées à partir de capteur de hello et envoyées tooyour Azure IoT hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualisation de données en temps réel, visualisation de données en direct, visualisation de données de capteurs"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="75290-104">Visualiser des données de capteur en temps réel depuis Azure IoT Hub, à l’aide de Power BI</span><span class="sxs-lookup"><span data-stu-id="75290-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="75290-106">Contenu</span><span class="sxs-lookup"><span data-stu-id="75290-106">What you learn</span></span>

<span data-ttu-id="75290-107">Vous apprendrez comment les données des capteurs en temps réel toovisualize votre concentrateur Azure IoT reçoit par Power BI.</span><span class="sxs-lookup"><span data-stu-id="75290-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="75290-108">Si vous souhaitez tootry visualiser les données de hello dans votre IoT hub avec des applications Web, consultez [données de capteur en temps réel toovisualize utilisation Azure Web Apps dans Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="75290-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="75290-109">Procédure</span><span class="sxs-lookup"><span data-stu-id="75290-109">What you do</span></span>

- <span data-ttu-id="75290-110">Préparez votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="75290-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="75290-111">Créer, configurer et exécuter une tâche de flux de données Analytique pour le transfert de données à partir de votre tooyour de hub IoT compte Power BI.</span><span class="sxs-lookup"><span data-stu-id="75290-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="75290-112">Créer et publier des données hello toovisualize d’un rapport Power BI.</span><span class="sxs-lookup"><span data-stu-id="75290-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="75290-113">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="75290-113">What you need</span></span>

- <span data-ttu-id="75290-114">Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="75290-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="75290-115">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="75290-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="75290-116">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="75290-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="75290-117">Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="75290-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="75290-118">Un compte Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="75290-118">A Power BI account.</span></span> <span data-ttu-id="75290-119">([Essayez Power BI gratuitement](https://powerbi.microsoft.com/)).</span><span class="sxs-lookup"><span data-stu-id="75290-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="75290-120">Créer, configurer et exécuter un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75290-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="75290-121">Création d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75290-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="75290-122">Dans l’hello portail Azure, cliquez sur Nouveau > Internet of Things > tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="75290-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="75290-123">Entrez hello informations pour le travail de hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="75290-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="75290-124">**Nom de la tâche**: nom hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="75290-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="75290-125">nom de Hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="75290-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="75290-126">**Groupe de ressources**: utilisez hello même groupe de ressources qui utilise de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="75290-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="75290-127">**Emplacement**: utilisez hello même emplacement que votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="75290-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="75290-128">**Code confidentiel toodashboard**: Activez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="75290-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Créer un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="75290-130">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="75290-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="75290-131">Ajouter une tâche de flux de données Analytique toohello d’entrée</span><span class="sxs-lookup"><span data-stu-id="75290-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="75290-132">Tâche de flux de données Analytique hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="75290-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="75290-133">Sous **Topologie du travail**, cliquez sur **Entrées**.</span><span class="sxs-lookup"><span data-stu-id="75290-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="75290-134">Bonjour **entrées** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="75290-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="75290-135">**Alias d’entrée**: alias unique de hello pour l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="75290-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="75290-136">**Source** : sélectionnez **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="75290-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="75290-137">**Groupe de consommateurs**: groupe de consommateurs hello sélectionnez vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="75290-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="75290-138">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="75290-138">Click **Create**.</span></span>

   ![Ajouter une tâche de flux de données Analytique tooa d’entrée dans Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="75290-140">Ajouter une tâche de flux de données Analytique toohello sortie</span><span class="sxs-lookup"><span data-stu-id="75290-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="75290-141">Sous **Topologie du travail**, cliquez sur **Sorties**.</span><span class="sxs-lookup"><span data-stu-id="75290-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="75290-142">Bonjour **sorties** volet, cliquez sur **ajouter**, puis entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="75290-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="75290-143">**Alias de sortie**: alias unique de hello pour la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="75290-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="75290-144">**Section sink**: sélectionnez **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="75290-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="75290-145">Cliquez sur **Autoriser**, puis connectez-vous à votre compte Power BI.</span><span class="sxs-lookup"><span data-stu-id="75290-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="75290-146">Une fois autorisé, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="75290-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="75290-147">**Espace de travail de groupe** : sélectionnez l’espace de travail de groupe cible.</span><span class="sxs-lookup"><span data-stu-id="75290-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="75290-148">**Nom du jeu de données** : saisissez le nom de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="75290-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="75290-149">**Nom de la table** : saisissez le nom de la table.</span><span class="sxs-lookup"><span data-stu-id="75290-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="75290-150">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="75290-150">Click **Create**.</span></span>

   ![Ajouter une tâche de flux de données Analytique sortie tooa dans Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="75290-152">Configurer la requête hello de tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="75290-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="75290-153">Sous **Topologie du travail**, cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="75290-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="75290-154">Remplacez `[YourInputAlias]` avec alias hello d’entrée de tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="75290-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="75290-155">Remplacez `[YourOutputAlias]` avec l’alias de sortie hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="75290-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="75290-156">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="75290-156">Click **Save**.</span></span>

   ![Ajouter une tâche de flux de données Analytique requête tooa dans Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="75290-158">Exécuter la tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="75290-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="75290-159">Dans la tâche de flux de données Analytique hello, cliquez sur **Démarrer** > **maintenant** > **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="75290-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="75290-160">Une fois le travail de hello démarre avec succès, état de la tâche hello passe de **arrêté** trop**en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="75290-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Exécuter un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="75290-162">Créer et publier des données hello toovisualize d’un rapport Power BI</span><span class="sxs-lookup"><span data-stu-id="75290-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="75290-163">Vérifiez l’application d’exemple hello est en cours d’exécution sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="75290-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="75290-164">Si non, vous pouvez faire référence à des didacticiels toohello sous [configurer votre appareil](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="75290-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="75290-165">Connectez-vous à tooyour [Power BI](https://powerbi.microsoft.com/en-us/) compte.</span><span class="sxs-lookup"><span data-stu-id="75290-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="75290-166">Atteindre l’espace de travail toohello groupe que vous définissez lors de la création de la sortie de hello pour la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="75290-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="75290-167">Cliquez sur **Jeux de données de diffusion en continu**.</span><span class="sxs-lookup"><span data-stu-id="75290-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="75290-168">Vous devez voir hello répertorié de jeu de données que vous avez spécifié lors de la création de hello de sortie pour la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="75290-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="75290-169">Sous **ACTIONS**, cliquez sur hello première icône toocreate un rapport.</span><span class="sxs-lookup"><span data-stu-id="75290-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Créer un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="75290-171">Créer une ligne graphique tooshow en temps réel de la température au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="75290-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="75290-172">Sur la page de création de rapports hello, ajoutez un graphique en courbes.</span><span class="sxs-lookup"><span data-stu-id="75290-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="75290-173">Sur hello **champs** volet, développez la table hello que vous avez spécifié lors de la création de sortie hello pour la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="75290-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="75290-174">Faites glisser **EventEnqueuedUtcTime** trop**axe** sur hello **visualisations** volet.</span><span class="sxs-lookup"><span data-stu-id="75290-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="75290-175">Faites glisser **température** trop**valeurs**.</span><span class="sxs-lookup"><span data-stu-id="75290-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="75290-176">Le graphique en courbes est désormais créé.</span><span class="sxs-lookup"><span data-stu-id="75290-176">Now a line chart is created.</span></span> <span data-ttu-id="75290-177">axe des abscisses Hello affiche la date et heure dans le fuseau horaire de hello UTC.</span><span class="sxs-lookup"><span data-stu-id="75290-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="75290-178">l’axe des y Hello affiche la température du capteur de hello.</span><span class="sxs-lookup"><span data-stu-id="75290-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Ajouter un graphique en courbes pour température tooa rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="75290-180">Créer un autre humidité en temps réel ligne graphique tooshow au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="75290-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="75290-181">toodo, suivez hello même les étapes ci-dessus et placez **EventEnqueuedUtcTime** sur l’axe des abscisses hello et **humidité** sur l’axe des y hello.</span><span class="sxs-lookup"><span data-stu-id="75290-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Ajouter un graphique en courbes pour humidité tooa rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="75290-183">Cliquez sur **enregistrer** rapport de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="75290-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="75290-184">Cliquez sur **fichier** > **publier tooweb**.</span><span class="sxs-lookup"><span data-stu-id="75290-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="75290-185">Cliquez sur **Créer le code incorporé**, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="75290-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="75290-186">Vous bénéficiez de lien de rapport hello que vous pouvez partager avec quiconque pour accéder au rapport et un rapport de hello toointegrate code extrait de code dans votre blog ou d’un site Web.</span><span class="sxs-lookup"><span data-stu-id="75290-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Publier un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="75290-188">Microsoft propose également hello [applications mobiles Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) pour afficher et interagir avec vos tableaux de bord Power BI et les rapports sur votre appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="75290-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75290-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="75290-189">Next steps</span></span>

<span data-ttu-id="75290-190">Vous avez utilisé avec succès données de capteur en temps réel toovisualize Power BI à partir de votre concentrateur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="75290-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="75290-191">Donnée une autre façon toovisualize à partir d’Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75290-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="75290-192">Consultez [données de capteur en temps réel toovisualize utilisation Azure Web Apps dans Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="75290-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
