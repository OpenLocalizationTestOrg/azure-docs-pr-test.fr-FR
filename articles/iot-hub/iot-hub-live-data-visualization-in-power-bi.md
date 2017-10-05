---
title: "Visualisation en temps réel des données de capteur depuis Azure IoT Hub : Power BI | Documents Microsoft"
description: "Power BI permet d’afficher des données sur les températures et l’humidité collectées par le capteur et envoyées à votre instance Azure IoT Hub."
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
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="3ac20-104">Visualiser des données de capteur en temps réel depuis Azure IoT Hub, à l’aide de Power BI</span><span class="sxs-lookup"><span data-stu-id="3ac20-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="3ac20-106">Contenu</span><span class="sxs-lookup"><span data-stu-id="3ac20-106">What you learn</span></span>

<span data-ttu-id="3ac20-107">Vous apprenez à visualiser les données de capteur en temps réel que votre instance Azure IoT Hub reçoit par l’intermédiaire de Power BI.</span><span class="sxs-lookup"><span data-stu-id="3ac20-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="3ac20-108">Si vous souhaitez essayer de visualiser les données dans votre instance IoT Hub avec Web Apps, consultez la rubrique [Utiliser Azure Web Apps pour visualiser les données de capteur en temps réel à partir d’Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3ac20-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3ac20-109">Procédure</span><span class="sxs-lookup"><span data-stu-id="3ac20-109">What you do</span></span>

- <span data-ttu-id="3ac20-110">Préparation de votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="3ac20-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="3ac20-111">Création, configuration et exécution d’un travail Stream Analytics pour le transfert de données depuis votre instance IoT Hub vers votre compte Power BI.</span><span class="sxs-lookup"><span data-stu-id="3ac20-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="3ac20-112">Création et publication d’un rapport Power BI pour visualiser les données.</span><span class="sxs-lookup"><span data-stu-id="3ac20-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3ac20-113">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="3ac20-113">What you need</span></span>

- <span data-ttu-id="3ac20-114">Le didacticiel [Configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé, qui traite des exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ac20-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="3ac20-115">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="3ac20-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="3ac20-116">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3ac20-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="3ac20-117">Une application cliente qui envoie des messages à votre instance Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3ac20-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="3ac20-118">Un compte Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="3ac20-118">A Power BI account.</span></span> <span data-ttu-id="3ac20-119">([Essayez Power BI gratuitement](https://powerbi.microsoft.com/)).</span><span class="sxs-lookup"><span data-stu-id="3ac20-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="3ac20-120">Créer, configurer et exécuter un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3ac20-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="3ac20-121">Création d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3ac20-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="3ac20-122">Dans le portail Azure, cliquez sur Nouveau > Internet des objets > Travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3ac20-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="3ac20-123">Saisissez les informations ci-après concernant le travail.</span><span class="sxs-lookup"><span data-stu-id="3ac20-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="3ac20-124">**Nom du travail** : nom du travail.</span><span class="sxs-lookup"><span data-stu-id="3ac20-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="3ac20-125">Le nom doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="3ac20-125">The name must be globally unique.</span></span>

   <span data-ttu-id="3ac20-126">**Groupe de ressources** : utilisez le groupe de ressources que votre instance IoT Hub exploite.</span><span class="sxs-lookup"><span data-stu-id="3ac20-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="3ac20-127">**Emplacement** : utilisez le même emplacement que votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3ac20-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="3ac20-128">**Épingler au tableau de bord** : cochez cette option pour pouvoir accéder facilement à votre instance IoT Hub à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="3ac20-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Créer un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="3ac20-130">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="3ac20-131">Ajouter une entrée au travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3ac20-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="3ac20-132">Ouvrez le travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3ac20-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="3ac20-133">Sous **Topologie du travail**, cliquez sur **Entrées**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="3ac20-134">Dans le volet **Entrées**, cliquez sur **Ajouter**, puis saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ac20-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="3ac20-135">**Alias d’entrée** : alias unique de l’entrée.</span><span class="sxs-lookup"><span data-stu-id="3ac20-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="3ac20-136">**Source** : sélectionnez **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="3ac20-137">**Groupe de consommateurs** : sélectionnez le groupe de consommateurs que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="3ac20-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="3ac20-138">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-138">Click **Create**.</span></span>

   ![Ajouter une entrée à un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="3ac20-140">Ajouter une sortie au travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3ac20-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="3ac20-141">Sous **Topologie du travail**, cliquez sur **Sorties**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="3ac20-142">Dans le volet **Sorties**, cliquez sur **Ajouter**, puis saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ac20-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="3ac20-143">**Alias de sortie** : alias unique de la sortie.</span><span class="sxs-lookup"><span data-stu-id="3ac20-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="3ac20-144">**Section sink**: sélectionnez **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="3ac20-145">Cliquez sur **Autoriser**, puis connectez-vous à votre compte Power BI.</span><span class="sxs-lookup"><span data-stu-id="3ac20-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="3ac20-146">Une fois authentifié, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ac20-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="3ac20-147">**Espace de travail de groupe** : sélectionnez l’espace de travail de groupe cible.</span><span class="sxs-lookup"><span data-stu-id="3ac20-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="3ac20-148">**Nom du jeu de données** : saisissez le nom de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="3ac20-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="3ac20-149">**Nom de la table** : saisissez le nom de la table.</span><span class="sxs-lookup"><span data-stu-id="3ac20-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="3ac20-150">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-150">Click **Create**.</span></span>

   ![Ajouter une sortie à un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="3ac20-152">Configurer la requête du travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3ac20-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="3ac20-153">Sous **Topologie du travail**, cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="3ac20-154">Remplacez `[YourInputAlias]` par l’alias d’entrée du travail.</span><span class="sxs-lookup"><span data-stu-id="3ac20-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="3ac20-155">Remplacez `[YourOutputAlias]` par l’alias de sortie du travail.</span><span class="sxs-lookup"><span data-stu-id="3ac20-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="3ac20-156">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-156">Click **Save**.</span></span>

   ![Ajouter une requête à un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="3ac20-158">Exécuter la tâche Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3ac20-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="3ac20-159">Dans le travail Stream Analytics, cliquez sur **Démarrer** > **Maintenant** > **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="3ac20-160">Une fois le travail lancé, l’état correspondant passe de **Arrêté** à **Exécution**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Exécuter un travail Stream Analytics dans Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="3ac20-162">Créer et publier un rapport Power BI pour visualiser les données</span><span class="sxs-lookup"><span data-stu-id="3ac20-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="3ac20-163">Vérifiez que l’exemple d’application s’exécute correctement sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="3ac20-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="3ac20-164">Si ce n’est pas le cas, vous pouvez consulter les didacticiels sous [Configurer votre appareil](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="3ac20-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="3ac20-165">Connectez-vous à votre compte [Power BI](https://powerbi.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="3ac20-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="3ac20-166">Accédez à l’espace de travail de groupe que vous définissez lors de la création de la sortie du travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3ac20-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="3ac20-167">Cliquez sur **Jeux de données de diffusion en continu**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="3ac20-168">Vous devez voir apparaître le jeu de données répertorié que vous avez indiqué lors de la création de la sortie du travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3ac20-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="3ac20-169">Sous **ACTIONS**, cliquez sur la première icône pour créer un rapport.</span><span class="sxs-lookup"><span data-stu-id="3ac20-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Créer un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="3ac20-171">Créez un graphique en courbes pour afficher la température en temps réel et au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="3ac20-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="3ac20-172">Sur la page de création du rapport, ajoutez un graphique en courbes.</span><span class="sxs-lookup"><span data-stu-id="3ac20-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="3ac20-173">Sur le volet **Champs**, développez la table que vous avez indiquée lors de la création de la sortie du travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3ac20-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="3ac20-174">Faites glisser **EventEnqueuedUtcTime** vers **Axe** dans le volet **Visualisations**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="3ac20-175">Faites glisser **Température** vers **Valeurs**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="3ac20-176">Le graphique en courbes est désormais créé.</span><span class="sxs-lookup"><span data-stu-id="3ac20-176">Now a line chart is created.</span></span> <span data-ttu-id="3ac20-177">L’axe des abscisses affiche la date et l’heure du fuseau horaire UTC.</span><span class="sxs-lookup"><span data-stu-id="3ac20-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="3ac20-178">Quant à l’axe des ordonnées, il affiche la température fournie par le capteur.</span><span class="sxs-lookup"><span data-stu-id="3ac20-178">The y-axis displays temperature from the sensor.</span></span>

      ![Ajouter un graphique en courbes sur la température dans un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="3ac20-180">Créez un autre graphique en courbes pour afficher l’humidité en temps réel, au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="3ac20-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="3ac20-181">Pour ce faire, suivez la procédure ci-dessus et placez **EventEnqueuedUtcTime** sur l’axe des abscisses et **Humidité** sur l’axe des ordonnées.</span><span class="sxs-lookup"><span data-stu-id="3ac20-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Ajouter un graphique en courbes sur l’humidité dans un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="3ac20-183">Cliquez sur **Enregistrer** pour enregistrer le rapport.</span><span class="sxs-lookup"><span data-stu-id="3ac20-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="3ac20-184">Cliquez sur **Fichier** > **Publier sur le web**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="3ac20-185">Cliquez sur **Créer le code incorporé**, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="3ac20-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="3ac20-186">Vous obtenez le lien d’accès au rapport, que vous pouvez partager avec les utilisateurs pour leur permettre d’y accéder, ainsi qu’un extrait de code, qui permet d’intégrer le rapport dans votre blog ou site web.</span><span class="sxs-lookup"><span data-stu-id="3ac20-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Publier un rapport Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="3ac20-188">Microsoft propose également des [applications mobiles Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/), qui permettent d’afficher les tableaux de bord et rapports Power BI sur votre appareil mobile et d’interagir avec eux.</span><span class="sxs-lookup"><span data-stu-id="3ac20-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ac20-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ac20-189">Next steps</span></span>

<span data-ttu-id="3ac20-190">Vous avez correctement utilisé Power BI pour visualiser les données de capteur en temps réel, à partir de votre instance Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3ac20-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="3ac20-191">Cela dit, il existe un autre moyen de visualiser ces données depuis Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3ac20-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="3ac20-192">Voir [Utiliser Azure Web Apps pour visualiser les données de capteur en temps réel à partir d’Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3ac20-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
