---
title: "Tableau de bord Power BI pour l’état des véhicules et les habitudes de conduite - Azure | Microsoft Docs"
description: "Utilisez les fonctionnalités de Cortana Intelligence pour obtenir des informations en temps réel et prédictives sur l’état des véhicules et les habitudes de conduite."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="ae1c2-103">Instructions de configuration du tableau de bord Power BI pour le modèle de la solution Vehicle Telemetry Analytics</span><span class="sxs-lookup"><span data-stu-id="ae1c2-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="ae1c2-104">Ce **menu** contient des liens vers les chapitres de ce manuel.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="ae1c2-105">La solution Vehicle Telemetry Analytics décrit la manière dont les concessions, constructeurs automobiles et compagnies d’assurance peuvent exploiter les fonctionnalités de Cortana Intelligence pour obtenir une visibilité en temps réel et prédictive sur l’état du véhicule et les habitudes de conduite, ce afin d’apporter des améliorations dans les domaines de l’expérience client, de la recherche et du développement, ainsi que des campagnes marketing.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="ae1c2-106">Ce document contient des instructions pas à pas sur la manière de configurer les rapports et le tableau de bord Power BI une fois la solution déployée dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ae1c2-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ae1c2-107">Prerequisites</span></span>
1. <span data-ttu-id="ae1c2-108">Déployer la solution [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="ae1c2-109">Installez Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="ae1c2-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="ae1c2-110">Un [abonnement Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae1c2-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="ae1c2-111">Si vous n’avez pas d’abonnement Azure, commencez par un abonnement Azure gratuit</span><span class="sxs-lookup"><span data-stu-id="ae1c2-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="ae1c2-112">Compte Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="ae1c2-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="ae1c2-113">Composants Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="ae1c2-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="ae1c2-114">Les services Cortana Intelligence suivants sont déployés dans votre abonnement parallèlement au modèle de solution Vehicle Telemetry Analytics.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="ae1c2-115">**Event Hubs** pour l’ingestion dans Azure de millions d’événements de télémétrie de véhicules.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="ae1c2-116">**STREAM ANALYTICS** , pour une visibilité en temps réel sur l’état des véhicules et une conservation de ces données dans un stockage à long terme afin d’enrichir les analyses par lots.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="ae1c2-117">**MACHINE LEARNING** , pour la détection d’anomalies en temps réel et le traitement par lots afin d’obtenir des informations prédictives.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="ae1c2-118">**HDInsight** est utilisé pour transformer les données à grande échelle</span><span class="sxs-lookup"><span data-stu-id="ae1c2-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="ae1c2-119">**Data Factory** gère l’orchestration, la planification, la gestion des ressources et la surveillance du pipeline de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="ae1c2-120">**POWER BI** offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="ae1c2-121">La solution utilise deux sources de données différentes : **jeu de données de diagnostics et de signaux des véhicules simulés** et **catalogue de véhicules**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="ae1c2-122">Un simulateur de télématique des véhicules est intégré à cette solution.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="ae1c2-123">Ce simulateur émet des informations de diagnostic et des signaux correspondant à l’état du véhicule et au schéma de conduite à un moment donné dans le temps.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="ae1c2-124">Le catalogue de véhicules est un jeu de données de référence contenant un mappage VIN/modèle</span><span class="sxs-lookup"><span data-stu-id="ae1c2-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="ae1c2-125">Préparation du tableau de bord Power BI</span><span class="sxs-lookup"><span data-stu-id="ae1c2-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="ae1c2-126">Configuration du tableau de bord Power BI en temps réel</span><span class="sxs-lookup"><span data-stu-id="ae1c2-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="ae1c2-127">**Démarrer l’application de tableau de bord en temps réel** Une fois le déploiement terminé, vous devez suivre les Instructions d’opération manuelle</span><span class="sxs-lookup"><span data-stu-id="ae1c2-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="ae1c2-128">Téléchargez l’application de tableau de bord en temps réel RealtimeDashboardApp.zip et décompressez-le.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="ae1c2-129">Dans le dossier décompressé, ouvrez le fichier de configuration d’application « RealtimeDashboardApp.exe.config », remplacez les appSettings pour les connexions de service EventHub, Stockage Blob et ML par les valeurs indiquées dans les Instructions d’opération manuelle, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="ae1c2-130">Exécutez l’application RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="ae1c2-131">Une fenêtre de connexion s’affiche. Entrez vos informations d’identification Power BI valides, puis cliquez sur le bouton **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="ae1c2-132">Ensuite, l’application commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-132">Then the app will start to run.</span></span>

   ![Connectez-vous à Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Autorisations du tableau de bord Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="ae1c2-135">Connectez-vous au site web de Power BI, puis créez le tableau de bord en temps réel.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="ae1c2-136">Vous êtes maintenant prêt à configurer le tableau de bord Power BI avec des visualisations enrichies pour obtenir des informations en temps réel et prédictives sur l’état des véhicules et les habitudes de conduite.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="ae1c2-137">Comptez de 45 minutes à une heure environ pour créer tous les rapports et configurer le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="ae1c2-138">Configurer les rapports Power BI</span><span class="sxs-lookup"><span data-stu-id="ae1c2-138">Configure Power BI reports</span></span>
<span data-ttu-id="ae1c2-139">Les rapports en temps réel et le tableau de bord prennent environ 30 à 45 minutes.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="ae1c2-140">Accédez à [http://powerbi.com](http://powerbi.com) et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Connectez-vous à Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="ae1c2-142">Un nouveau jeu de données est généré dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="ae1c2-143">Cliquez sur le jeu de données **ConnectedCarsRealtime** .</span><span class="sxs-lookup"><span data-stu-id="ae1c2-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Jeu de données Connected Cars en temps réel sélectionné](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="ae1c2-145">Enregistrez le rapport vierge à l’aide de la combinaison **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-145">Save the blank report using **Ctrl + s**.</span></span>

![Enregistrez le rapport vide](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="ae1c2-147">Nommez le rapport *Vehicle Telemetry Analytics Real-time - Reports*.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Nommez le rapport](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="ae1c2-149">Rapports en temps réel</span><span class="sxs-lookup"><span data-stu-id="ae1c2-149">Real-time reports</span></span>
<span data-ttu-id="ae1c2-150">Il existe trois rapports en temps réel dans cette solution :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="ae1c2-151">Véhicules opérationnels</span><span class="sxs-lookup"><span data-stu-id="ae1c2-151">Vehicles in operation</span></span>
2. <span data-ttu-id="ae1c2-152">Véhicules nécessitant une maintenance</span><span class="sxs-lookup"><span data-stu-id="ae1c2-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="ae1c2-153">Statistiques relatives à l’état des véhicules</span><span class="sxs-lookup"><span data-stu-id="ae1c2-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="ae1c2-154">Vous pouvez choisir de configurer les trois rapports en temps réel, ou arrêter après l’étape de votre choix et passer à la section suivante de la configuration des rapports de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="ae1c2-155">Nous vous recommandons de créer les trois rapports afin de visualiser toutes les informations de la fonction temps réel de la solution.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="ae1c2-156">1. Véhicules opérationnels</span><span class="sxs-lookup"><span data-stu-id="ae1c2-156">1. Vehicles in operation</span></span>
<span data-ttu-id="ae1c2-157">Double-cliquez sur la **Page 1** et renommez-la « Véhicules opérationnels ».</span><span class="sxs-lookup"><span data-stu-id="ae1c2-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="ae1c2-158">![Connected Cars - Véhicules opérationnels](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="ae1c2-159">Sélectionnez **vin** dans **Champs** et choisissez **« Carte »** comme type de visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="ae1c2-160">Une visualisation sous forme de carte est créée, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-160">Card visualization is created as shown in figure.</span></span>  
    ![Connected Cars - Sélectionner le numéro d’identification du véhicule](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="ae1c2-162">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="ae1c2-163">Sélectionnez **Ville** et **vin** dans Champs.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="ae1c2-164">Choisissez la visualisation de type **« Carte »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="ae1c2-165">Faites glisser **vin** dans la zone de valeurs.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-165">Drag **vin** in values area.</span></span> <span data-ttu-id="ae1c2-166">Faites glisser **city** vers la zone **Legend**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="ae1c2-167">![Connected Cars - Visualisation sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="ae1c2-168">Sélectionnez la section **Format** dans **Visualisations**, puis cliquez sur **Titre** et modifiez le **texte** en le remplaçant par **« Véhicules opérationnels par ville »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="ae1c2-169">![Connected Cars - Véhicules opérationnels par ville](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="ae1c2-170">La visualisation finale doit être telle qu’illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-170">Final visualization looks as shown in figure.</span></span>    
    ![Connected Cars - Visualisation finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="ae1c2-172">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="ae1c2-173">Sélectionnez **Ville** et **vin**, puis modifiez le type de visualisation en lui affectant la valeur **Histogramme groupé**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="ae1c2-174">Vérifiez le champ **Ville** dans la zone **Axe** et **vin** dans la zone **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="ae1c2-175">Triez le graphique par **« Nombre de vin »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="ae1c2-176">![Connected Cars - Nombre de numéros d’identification de véhicule](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="ae1c2-177">Modifiez le **titre** du graphique en le nommant **« Véhicules opérationnels par ville »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="ae1c2-178">Cliquez sur la section **Format**, puis sélectionnez **Couleurs des données**. Cliquez sur **« Activé »** dans **Afficher tout**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="ae1c2-179">![Connected Cars - Afficher toutes les couleurs de données](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="ae1c2-180">Modifiez la couleur de chaque ville en cliquant sur l’icône de couleur.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Connected Cars - Modifier les couleurs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="ae1c2-182">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="ae1c2-183">Sélectionnez la visualisation **Histogramme groupé** dans la zone Visualisations, faites glisser le champ **Ville** dans la zone **Axe**, **Modèle** dans la zone **Légende** et **vin** dans la zone **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="ae1c2-184">![Connected Cars - Histogramme groupé](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="ae1c2-185">![Connected Cars - Rendu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="ae1c2-186">Réorganisez toutes les visualisations sur cette page comme indiqué dans la figure.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Connected Cars - Visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="ae1c2-188">Vous avez correctement configuré le rapport en temps réel « Véhicules opérationnels ».</span><span class="sxs-lookup"><span data-stu-id="ae1c2-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="ae1c2-189">Vous pouvez passer à la création du rapport en temps réel suivant, ou bien vous arrêter ici et configurer le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="ae1c2-190">2. Véhicules nécessitant une maintenance</span><span class="sxs-lookup"><span data-stu-id="ae1c2-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="ae1c2-191">Cliquez sur ![Ajouter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) pour ajouter un nouveau rapport, puis renommez-le **« Véhicules nécessitant une maintenance »**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Connected Cars - Véhicules nécessitant une maintenance](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="ae1c2-193">Sélectionnez le champ **vin** et définissez le type de visualisation sur **Carte**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="ae1c2-194">![Connected Cars - Visualisation du numéro d’identification du véhicule sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="ae1c2-195">Le jeu de données contient un champ nommé « MaintenanceLabel ».</span><span class="sxs-lookup"><span data-stu-id="ae1c2-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="ae1c2-196">Ce champ peut avoir une valeur de « 0 » ou « 1 ».</span><span class="sxs-lookup"><span data-stu-id="ae1c2-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="ae1c2-197">Il est défini par le modèle Azure Machine Learning configuré dans le cadre de la solution et intégré avec la fonction temps réel.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="ae1c2-198">La valeur « 1 » indique un véhicule nécessitant une maintenance.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="ae1c2-199">Pour ajouter le filtre **Page Level** (Niveau page) afin d’afficher les données relatives aux véhicules ayant besoin d’une intervention de maintenance :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="ae1c2-200">Faites glisser le champ **« MaintenanceLabel »** dans **Filtres de niveau page**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="ae1c2-201">![Connected Cars - Filtres au niveau de la page](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="ae1c2-202">Cliquez sur le menu **Filtrage de base** situé en bas du filtre de niveau page MaintenanceLabel.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="ae1c2-203">![Connected Cars - Filtrage de base](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="ae1c2-204">Affectez-lui la valeur de filtre **« 1 »**  </span><span class="sxs-lookup"><span data-stu-id="ae1c2-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="ae1c2-205">![Connected Cars - Valeur de filtre](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="ae1c2-206">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="ae1c2-207">Sélectionnez **Histogramme groupé** dans la section Visualisations.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="ae1c2-208">![Connected Cars - Visualisation du numéro d’identification du véhicule sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="ae1c2-209">![Connected Cars - Histogramme groupé](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="ae1c2-210">Faites glisser le champ **Modèle** dans la zone **Axe** et le champ **Vin** dans la zone **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="ae1c2-211">Triez ensuite la visualisation par **Nombre de vin**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="ae1c2-212">Modifiez le **titre** du graphique en le renommant **« Véhicules nécessitant une maintenance par modèle »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="ae1c2-213">Faites glisser les champs **vin** dans la zone **Saturation de la couleur** située dans la section **Champs** ![Champs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png)de l’onglet **Visualisation**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="ae1c2-214">![Connected Cars - Saturation des couleurs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="ae1c2-215">Modifiez **Couleurs des données** dans les visualisations à partir de la section **Format**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="ae1c2-216">Définissez **F2C812** comme couleur minimale.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="ae1c2-217">Définissez **FF6300** comme couleur maximale.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="ae1c2-218">![Connected Cars - Changements de couleur](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="ae1c2-219">![Connected Cars - Nouvelles couleurs de visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="ae1c2-220">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="ae1c2-221">Sélectionnez **Histogramme groupé** dans la zone Visualisations, faites glisser le champ **vin** dans la zone **Valeur** et le champ **Ville** dans la zone **Axe**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="ae1c2-222">Triez le graphique par **« Nombre de vin »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="ae1c2-223">Modifiez le **titre** du graphique en le renommant **« Véhicules nécessitant une maintenance par ville »** </span><span class="sxs-lookup"><span data-stu-id="ae1c2-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="ae1c2-224">![Connected Cars - Véhicules nécessitant une maintenance par ville](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="ae1c2-225">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="ae1c2-226">Dans la section Visualisations, sélectionnez la visualisation **Carte à plusieurs lignes**, puis faites glisser les champs **Modèle** et **vin** dans la zone **Champs**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="ae1c2-227">![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="ae1c2-228">En réorganisant l’ensemble de la visualisation, le rapport final se présente comme suit : </span><span class="sxs-lookup"><span data-stu-id="ae1c2-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="ae1c2-230">Vous avez correctement configuré le rapport en temps réel « Véhicules nécessitant une maintenance ».</span><span class="sxs-lookup"><span data-stu-id="ae1c2-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="ae1c2-231">Vous pouvez passer à la création du rapport en temps réel suivant, ou bien vous arrêter ici et configurer le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="ae1c2-232">3. Statistiques relatives à l’état des véhicules</span><span class="sxs-lookup"><span data-stu-id="ae1c2-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="ae1c2-233">Cliquez sur ![Ajouter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) pour ajouter un rapport, puis renommez-le **« Statistiques relatives à l’état des véhicules »**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="ae1c2-234">Dans la section Visualisations, sélectionnez la visualisation **Jauge**, puis faites glisser le champ **Vitesse** dans les zones **Valeur, Valeur minimum, Valeur maximum**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="ae1c2-235">![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="ae1c2-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="ae1c2-236">Modifiez l’agrégation par défaut du champ **Vitesse** dans la zone **Valeur** en lui affectant la valeur **Moyenne**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="ae1c2-237">Modifiez l’agrégation par défaut du champ **Vitesse** dans la zone **Minimum** en lui affectant la valeur **Minimum**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="ae1c2-238">Modifiez l’agrégation par défaut du champ **Vitesse** dans la zone **Maximum** en lui affectant la valeur **Maximum**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="ae1c2-240">Modifiez le **titre de la jauge** en **« Vitesse moyenne »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Connected Cars - Jauge](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="ae1c2-242">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="ae1c2-243">Vous pouvez également ajouter une **jauge** pour l’**huile moteur moyenne**, le **carburant moyen** et la **température moteur moyenne**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="ae1c2-244">Modifiez l’agrégation par défaut des champs de chaque jauge comme indiqué ci-dessus dans la jauge **« Vitesse moyenne »** .</span><span class="sxs-lookup"><span data-stu-id="ae1c2-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Connected Cars - Jauges](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="ae1c2-246">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="ae1c2-247">Dans la section Visualisations, sélectionnez **Graphique en courbes et histogramme groupé**, puis faites glisser le champ **Ville** dans la zone **Axe partagé** et les champs **Vitesse**, **Pression des pneus et Huile moteur** dans la zone **Valeurs de colonne**, puis définissez le type d’agrégation sur **Moyenne**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="ae1c2-248">Faites glisser le champ **Température moteur** dans la zone **Valeurs de ligne** et définissez le type d’agrégation sur **Moyenne**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Connected Cars - Champs de visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="ae1c2-250">Modifiez le **titre** du graphique en le renommant **« Vitesse moyenne, pression des pneus, huile moteur et température moteur »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Connected Cars - Champs de visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="ae1c2-252">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="ae1c2-253">Dans la section Visualisations, sélectionnez la visualisation **Compartimentage**, puis faites glisser le champ **Modèle** dans la zone **Groupe** et le champ **Probabilité de maintenance** dans la zone **Valeurs**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="ae1c2-254">Renommez le **titre** du graphique **« Modèles de véhicules nécessitant une maintenance »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="ae1c2-256">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="ae1c2-257">Dans la section Visualisations, sélectionnez **Graphique à barres empilées 100 %**, puis faites glisser le champ **Ville** dans la zone **Axe** et les champs **Probabilité de maintenance** et **Probabilité de rappel** dans la zone **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="ae1c2-259">Cliquez sur **Format**, sélectionnez **Couleurs des données**, puis affectez la valeur **« F2C80F »** à la couleur **Probabilité de maintenance**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="ae1c2-260">Renommez le **titre** du graphique **« Probabilité de maintenance et de rappel de véhicules par ville »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="ae1c2-262">Cliquez sur la zone vide pour ajouter la nouvelle visualisation.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="ae1c2-263">Dans la section Visualisations, sélectionnez la visualisation **Graphique en aires**, puis faites glisser le champ **Modèle** dans la zone **Axe** et les champs **Huile moteur, Pression des pneus, Vitesse et Probabilité de maintenance** dans la zone **Valeurs**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="ae1c2-264">Définissez le type d’agrégation sur **« Moyenne »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-264">Change their aggregation type to **“Average”**.</span></span> 

![Connected Cars - Modifier le type d’agrégation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="ae1c2-266">Modifiez le titre du graphique en le renommant **« Moyenne d’huile moteur, de pression des pneus et de vitesse et probabilité de maintenance par modèle »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="ae1c2-268">Cliquez sur la zone vide pour ajouter la nouvelle visualisation :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="ae1c2-269">Dans la section Visualisations, sélectionnez **Nuage de points** .</span><span class="sxs-lookup"><span data-stu-id="ae1c2-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="ae1c2-270">Faites glisser le champ **Modèle** dans les zones **Détails** et **Légende**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="ae1c2-271">Faites glisser le champ **Carburant** dans la zone **Axe des abscisses** et définissez l’agrégation sur **Moyenne**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="ae1c2-272">Faites glisser le champ **Température moteur** dans la zone **Axe des ordonnées** et définissez l’agrégation sur **Moyenne**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="ae1c2-273">Faites glisser le champ **vin** dans la zone **Taille**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-273">Drag the **vin** field into the **Size** area.</span></span>

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="ae1c2-275">Modifiez le **titre** du graphique en le renommant **«  Moyennes de carburant et de température moteur par modèle »**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="ae1c2-277">Le rapport final doit être similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-277">The final report will look like as shown below.</span></span>

![Connected Cars - Rapport final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="ae1c2-279">Épingler les visualisations des rapports sur le tableau de bord en temps réel</span><span class="sxs-lookup"><span data-stu-id="ae1c2-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="ae1c2-280">Créez un tableau de bord vide en cliquant sur l’icône « plus » en regard des tableaux de bord.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="ae1c2-281">Vous pouvez le nommer « Vehicle Telemetry - Tableau de bord d’analyse ».</span><span class="sxs-lookup"><span data-stu-id="ae1c2-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="ae1c2-283">Épinglez la visualisation des rapports ci-dessus au tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="ae1c2-285">Le tableau de bord doit se présenter comme illustré ci-après, lorsque les trois rapports sont créés et que les visualisations correspondantes sont épinglées à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="ae1c2-286">Si vous n’avez pas créé tous les rapports, l’apparence de votre tableau de bord peut différer.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="ae1c2-288">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ae1c2-288">Congratulations!</span></span> <span data-ttu-id="ae1c2-289">Vous avez correctement créé le tableau de bord en temps réel.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="ae1c2-290">Tandis que vous continuez pour exécuter CarEventGenerator.exe et RealtimeDashboardApp.exe, vous devez voir les mises à jour en direct sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="ae1c2-291">La procédure suivante doit prendre environ 10 à 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="ae1c2-292">Configuration du tableau de bord de traitement par lots de Power BI</span><span class="sxs-lookup"><span data-stu-id="ae1c2-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="ae1c2-293">Une fois le déploiement effectué, comptez environ deux heures pour permettre au pipeline de traitement par lots de terminer son exécution et de traiter l’équivalent d’une année de données générées.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="ae1c2-294">Attendez donc que le traitement se termine avant de passer aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="ae1c2-295">**Télécharger le fichier Power BI Designer**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="ae1c2-296">Un fichier Power BI Designer préconfiguré est inclus dans les Instructions d’opération manuelle du déploiement</span><span class="sxs-lookup"><span data-stu-id="ae1c2-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="ae1c2-297">Recherchez 2.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-297">Look for 2.</span></span> <span data-ttu-id="ae1c2-298">Installez le tableau de bord du traitement par lots de Power BI Vous pouvez télécharger le modèle Power BI pour le tableau de bord de traitement par lots appelé **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="ae1c2-299">Enregistrez le fichier en local</span><span class="sxs-lookup"><span data-stu-id="ae1c2-299">Save locally</span></span>

<span data-ttu-id="ae1c2-300">**Configurer les rapports Power BI**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="ae1c2-301">Ouvrez le fichier de concepteur « **ConnectedCarsPbiReport.pbix** » à l’aide de Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="ae1c2-302">Le cas échéant, installez Power BI Desktop depuis [PowerBI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="ae1c2-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="ae1c2-303">Cliquez sur **Modifier des requêtes**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-303">Click the **Edit Queries**.</span></span>

![Modifier une requête Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="ae1c2-305">Double-cliquez sur la **Source**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-305">Double-click the **Source**.</span></span>

![Définir la source Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="ae1c2-307">Mettez à jour la chaîne de connexion serveur avec le serveur SQL Azure que vous avez provisionné dans le cadre du déploiement.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="ae1c2-308">Recherchez dans les Instructions d’opération manuelle sous</span><span class="sxs-lookup"><span data-stu-id="ae1c2-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="ae1c2-309">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ae1c2-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="ae1c2-310">Serveur : somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="ae1c2-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="ae1c2-311">Base de données : connectedcar</span><span class="sxs-lookup"><span data-stu-id="ae1c2-311">Database: connectedcar</span></span>
    * <span data-ttu-id="ae1c2-312">Nom d’utilisateur : nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ae1c2-312">Username: username</span></span>
    * <span data-ttu-id="ae1c2-313">Mot de passe : vous pouvez gérer votre mot de passe SQL Server à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae1c2-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="ae1c2-314">Laissez la **base de données** en tant que *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-314">Leave **Database** as *connectedcar*.</span></span>

![Définir la base de données Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="ae1c2-316">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-316">Click **OK**.</span></span>
* <span data-ttu-id="ae1c2-317">L’onglet **Informations d’identification Windows** est sélectionné par défaut. Basculez sur **Informations d’identification de la base de données** en cliquant sur l’onglet **Base de données** situé à droite.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="ae1c2-318">Indiquez le **nom d’utilisateur** et le **mot de passe** de votre base de données SQL Azure renseignés pendant la configuration du déploiement.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Fournir les informations d’identification de la base de données](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="ae1c2-320">Cliquez sur **Connexion**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-320">Click **Connect**</span></span>
* <span data-ttu-id="ae1c2-321">Répétez les étapes ci-dessus pour chacune des trois requêtes restantes présentes sur le volet de droite, puis mettez à jour les informations de connexion de la source de données.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="ae1c2-322">Cliquez sur **Fermer et charger**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-322">Click **Close and Load**.</span></span> <span data-ttu-id="ae1c2-323">Les jeux de données de fichier Power BI Desktop sont connectés à des tables de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="ae1c2-324">**Fermez** le fichier Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-324">**Close** Power BI Desktop file.</span></span>

![Fermez Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="ae1c2-326">Cliquez sur **Enregistrer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="ae1c2-327">Vous avez maintenant configuré tous les rapports correspondant au traitement par lots dans la solution.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="ae1c2-328">Chargez les éléments vers *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="ae1c2-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="ae1c2-329">Accédez au portail web Power BI à l’adresse http://powerbi.com et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="ae1c2-330">Cliquez sur **Get Data**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="ae1c2-331">Chargez le fichier Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="ae1c2-332">Pour lancer le chargement, cliquez sur **Get Data (Obtenir les données) -> Files Get (Obtention de fichiers) -> Fichier local**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="ae1c2-333">Accédez au fichier « **“**ConnectedCarsPbiReport.pbix**“** »</span><span class="sxs-lookup"><span data-stu-id="ae1c2-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="ae1c2-334">Une fois le fichier chargé, vous serez redirigé vers votre espace de travail Power BI.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="ae1c2-335">Un jeu de données, un rapport et un tableau de bord vide sont alors créés.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="ae1c2-336">Épinglez les graphiques au nouveau tableau de bord **Vehicle Telemetry - Tableau de bord d’analyse** dans **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="ae1c2-337">Cliquez sur le tableau de bord vide que vous avez créé ci-dessus et accédez à la section **Rapports**. Cliquez sur le rapport que vous venez de charger.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="ae1c2-339">**Notez que le rapport contient six pages :**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="ae1c2-340">Page 1 : densité de véhicules</span><span class="sxs-lookup"><span data-stu-id="ae1c2-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="ae1c2-341">Page 2 : intégrité des véhicules en temps réel</span><span class="sxs-lookup"><span data-stu-id="ae1c2-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="ae1c2-342">Page 3 : véhicules utilisés de manière intensive</span><span class="sxs-lookup"><span data-stu-id="ae1c2-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="ae1c2-343">Page 4 : véhicules rappelés</span><span class="sxs-lookup"><span data-stu-id="ae1c2-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="ae1c2-344">Page 5 : véhicules économes en carburant</span><span class="sxs-lookup"><span data-stu-id="ae1c2-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="ae1c2-345">Page 6 : logo de Contoso</span><span class="sxs-lookup"><span data-stu-id="ae1c2-345">Page 6: Contoso Logo</span></span>  

![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="ae1c2-347">**À partir de la Page 3**, épinglez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="ae1c2-348">Nombre de vin</span><span class="sxs-lookup"><span data-stu-id="ae1c2-348">Count of VIN</span></span>  
   ![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="ae1c2-350">Véhicules utilisés de manière intensive par modèle – Graphique en cascade </span><span class="sxs-lookup"><span data-stu-id="ae1c2-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="ae1c2-352">**À partir de la Page 5**, épinglez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="ae1c2-353">Nombre de vin</span><span class="sxs-lookup"><span data-stu-id="ae1c2-353">Count of vin</span></span>    
   ![Vehicle Telemetry - Épingler des graphiques 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="ae1c2-355">Véhicules économes en carburant par modèle : histogramme groupé </span><span class="sxs-lookup"><span data-stu-id="ae1c2-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="ae1c2-357">**À partir de la Page 4**, épinglez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="ae1c2-358">Nombre de vin</span><span class="sxs-lookup"><span data-stu-id="ae1c2-358">Count of vin</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="ae1c2-360">Véhicules rappelés par ville, modèle : Compartimentage </span><span class="sxs-lookup"><span data-stu-id="ae1c2-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="ae1c2-362">**À partir de la Page 6**, épinglez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae1c2-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="ae1c2-363">Logo Contoso Motors </span><span class="sxs-lookup"><span data-stu-id="ae1c2-363">Contoso Motors logo</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="ae1c2-365">**Organiser le tableau de bord**</span><span class="sxs-lookup"><span data-stu-id="ae1c2-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="ae1c2-366">Accédez au tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="ae1c2-367">Placez le curseur sur chaque graphique et renommez-les selon les noms indiqués dans l’image complète du tableau de bord ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="ae1c2-368">Déplacez également les graphiques de manière à obtenir un tableau de bord similaire à la capture ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Vehicle Telemetry - Organiser le tableau de bord 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="ae1c2-371">Si vous avez créé tous les rapports comme indiqué dans ce document, le tableau de bord terminé final doit ressembler à la figure suivante.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Vehicle Telemetry - Organiser le tableau de bord 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="ae1c2-373">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ae1c2-373">Congratulations!</span></span> <span data-ttu-id="ae1c2-374">Vous avez correctement créé les rapports et le tableau de bord pour obtenir des informations en temps réel, prédictives et par lots sur l’état des véhicules et les habitudes de conduite.</span><span class="sxs-lookup"><span data-stu-id="ae1c2-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
