---
title: "aaaPower tableau de bord d’intégrité du véhicule et du pilotage habituelles - Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de hello des aperçus Cortana Intelligence toogain prédictives et en temps réel sur l’intégrité du véhicule et du pilotage habituelles."
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
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="bbb5e-103">Instructions de configuration du tableau de bord Power BI pour le modèle de la solution Vehicle Telemetry Analytics</span><span class="sxs-lookup"><span data-stu-id="bbb5e-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="bbb5e-104">Cela **menu** lie chapitres toohello dans ce manuel.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="bbb5e-105">Hello solution du véhicule télémétrie Analytique présente comment les concessions de voiture, constructeurs automobiles et aux entreprises d’assurance peuvent tirer parti des fonctionnalités de hello de Cortana Intelligence toogain prédictives et en temps réel des informations sur l’intégrité du véhicule et du pilotage améliorations de toodrive habitudes dans la zone de hello du client expérience, R & D et campagnes marketing.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="bbb5e-106">Ce document contient des instructions étape par étape sur la configuration des rapports de Power BI hello et tableau de bord une fois la solution de hello est déployée dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bbb5e-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bbb5e-107">Prerequisites</span></span>
1. <span data-ttu-id="bbb5e-108">Déployer hello [Analytique de télémétrie](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span><span class="sxs-lookup"><span data-stu-id="bbb5e-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="bbb5e-109">Installez Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="bbb5e-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="bbb5e-110">Un [abonnement Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbb5e-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="bbb5e-111">Si vous n’avez pas d’abonnement Azure, commencez par un abonnement Azure gratuit</span><span class="sxs-lookup"><span data-stu-id="bbb5e-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="bbb5e-112">Compte Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="bbb5e-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="bbb5e-113">Composants Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="bbb5e-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="bbb5e-114">Dans le cadre du modèle de solution hello véhicule télémétrie Analytique, hello suivant Cortana Intelligence services est déployé dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="bbb5e-115">**Event Hubs** pour l’ingestion dans Azure de millions d’événements de télémétrie de véhicules.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="bbb5e-116">**STREAM ANALYTICS** , pour une visibilité en temps réel sur l’état des véhicules et une conservation de ces données dans un stockage à long terme afin d’enrichir les analyses par lots.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="bbb5e-117">**Apprentissage** pour la détection d’anomalie en temps réel et les analyses prédictives toogain de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="bbb5e-118">**HDInsight** est exploitée tootransform des données à grande échelle</span><span class="sxs-lookup"><span data-stu-id="bbb5e-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="bbb5e-119">**Fabrique de données** gère l’orchestration, la planification, la gestion des ressources et la surveillance de pipeline de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="bbb5e-120">**POWER BI** offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="bbb5e-121">solution de Hello utilise deux sources de données différentes : **simulée véhicule signaux et le jeu de données de diagnostic** et **catalogue du véhicule**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="bbb5e-122">Un simulateur de télématique des véhicules est intégré à cette solution.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="bbb5e-123">Il émet des informations de diagnostic et signale un état toohello correspondant du véhicule de hello et modèle conduite à un moment donné dans le temps.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="bbb5e-124">Hello véhicule catalogue est un mappage de toomodel référence dataset contenant VIN</span><span class="sxs-lookup"><span data-stu-id="bbb5e-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="bbb5e-125">Préparation du tableau de bord Power BI</span><span class="sxs-lookup"><span data-stu-id="bbb5e-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="bbb5e-126">Configuration du tableau de bord Power BI en temps réel</span><span class="sxs-lookup"><span data-stu-id="bbb5e-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="bbb5e-127">**Démarrer l’application de tableau de bord en temps réel hello** une fois le déploiement de hello est terminé, vous devez suivre les Instructions de fonctionnement de manuel de hello</span><span class="sxs-lookup"><span data-stu-id="bbb5e-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="bbb5e-128">Téléchargez l’application de tableau de bord en temps réel RealtimeDashboardApp.zip et décompressez-le.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="bbb5e-129">Dans le dossier de décompressé hello, ouvrez le fichier de configuration d’application 'RealtimeDashboardApp.exe.config', appSettings de remplacement pour les connexions de service Eventhub, stockage d’objets Blob et ML avec des valeurs hello Bonjour Instructions d’opération manuelle, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="bbb5e-130">Exécutez l’application RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="bbb5e-131">Une fenêtre de connexion contextuelle, fournissez vos informations d’identification valides pour Power BI et cliquez sur hello **accepter** bouton.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="bbb5e-132">Ensuite, application hello démarre toorun.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-132">Then hello app will start toorun.</span></span>

   ![Connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Autorisations du tableau de bord Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="bbb5e-135">Site Web de connexion tooPowerBI et créer le tableau de bord en temps réel.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="bbb5e-136">Maintenant, vous êtes prêt tooconfigure hello tableau de bord avec toogain visualisations enrichies en temps réel et des analyses prédictives sur l’intégrité du véhicule et du pilotage habituelles.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="bbb5e-137">Il prend environ 45 minutes tooan heure toocreate hello tous les rapports et configurer le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="bbb5e-138">Configurer les rapports Power BI</span><span class="sxs-lookup"><span data-stu-id="bbb5e-138">Configure Power BI reports</span></span>
<span data-ttu-id="bbb5e-139">les rapports en temps réel Hello et tableau de bord hello prennent environ 30 et 45 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="bbb5e-140">Parcourir trop[http://powerbi.com](http://powerbi.com) et de la connexion.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="bbb5e-142">Un nouveau jeu de données est généré dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="bbb5e-143">Cliquez sur hello **ConnectedCarsRealtime** jeu de données.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Jeu de données Connected Cars en temps réel sélectionné](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="bbb5e-145">Enregistrer à l’aide de rapport vide hello **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-145">Save hello blank report using **Ctrl + s**.</span></span>

![Enregistrez le rapport vide](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="bbb5e-147">Nommez le rapport *Vehicle Telemetry Analytics Real-time - Reports*.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Nommez le rapport](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="bbb5e-149">Rapports en temps réel</span><span class="sxs-lookup"><span data-stu-id="bbb5e-149">Real-time reports</span></span>
<span data-ttu-id="bbb5e-150">Il existe trois rapports en temps réel dans cette solution :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="bbb5e-151">Véhicules opérationnels</span><span class="sxs-lookup"><span data-stu-id="bbb5e-151">Vehicles in operation</span></span>
2. <span data-ttu-id="bbb5e-152">Véhicules nécessitant une maintenance</span><span class="sxs-lookup"><span data-stu-id="bbb5e-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="bbb5e-153">Statistiques relatives à l’état des véhicules</span><span class="sxs-lookup"><span data-stu-id="bbb5e-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="bbb5e-154">Vous pouvez choisir tooconfigure tous les rapports en temps réel trois hello ou arrêter après n’importe quelle étape et continuer toohello la section suivante de la configuration des rapports de lot hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="bbb5e-155">Nous vous recommandons de vous toocreate tous les hello trois rapports insights complète de toovisualize hello du chemin d’accès en temps réel de hello de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="bbb5e-156">1. Véhicules opérationnels</span><span class="sxs-lookup"><span data-stu-id="bbb5e-156">1. Vehicles in operation</span></span>
<span data-ttu-id="bbb5e-157">Double-cliquez sur **Page 1** et renommez-la trop « Véhicules dans l’opération. »</span><span class="sxs-lookup"><span data-stu-id="bbb5e-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="bbb5e-158">![Connected Cars - Véhicules opérationnels](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="bbb5e-159">Sélectionnez **vin** dans **Champs** et choisissez **« Carte »** comme type de visualisation.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="bbb5e-160">Une visualisation sous forme de carte est créée, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-160">Card visualization is created as shown in figure.</span></span>  
    ![Connected Cars - Sélectionner le numéro d’identification du véhicule](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="bbb5e-162">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="bbb5e-163">Sélectionnez **Ville** et **vin** dans Champs.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="bbb5e-164">Changez de visualisation trop**« Mappage »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="bbb5e-165">Faites glisser **vin** dans la zone de valeurs.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-165">Drag **vin** in values area.</span></span> <span data-ttu-id="bbb5e-166">Faites glisser **Ville** à partir des champs trop**légende** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="bbb5e-167">![Connected Cars - Visualisation sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="bbb5e-168">Sélectionnez **format** section **visualisations**, cliquez sur **titre** et modifiez hello **texte** trop**véhicules » dans opération par ville »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="bbb5e-169">![Connected Cars - Véhicules opérationnels par ville](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="bbb5e-170">La visualisation finale doit être telle qu’illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-170">Final visualization looks as shown in figure.</span></span>    
    ![Connected Cars - Visualisation finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="bbb5e-172">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="bbb5e-173">Sélectionnez **Ville** et **vin**, modifiez le type de visualisation trop**Histogramme groupé**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="bbb5e-174">Vérifiez le champ **Ville** dans la zone **Axe** et **vin** dans la zone **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="bbb5e-175">Triez le graphique par **« Nombre de vin »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="bbb5e-176">![Connected Cars - Nombre de numéros d’identification de véhicule](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="bbb5e-177">Graphique de modification **titre** trop**« Véhicules dans l’opération par ville »**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="bbb5e-178">Cliquez sur hello **Format** section, puis sélectionnez **couleurs des données**, cliquez sur hello **« Sur »** trop**afficher tout**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="bbb5e-179">![Connected Cars - Afficher toutes les couleurs de données](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="bbb5e-180">Modifier la couleur hello de ville individuel en cliquant sur l’icône de couleur.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Connected Cars - Modifier les couleurs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="bbb5e-182">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="bbb5e-183">Sélectionnez la visualisation **Histogramme groupé** dans la zone Visualisations, faites glisser le champ **Ville** dans la zone **Axe**, **Modèle** dans la zone **Légende** et **vin** dans la zone **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="bbb5e-184">![Connected Cars - Histogramme groupé](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="bbb5e-185">![Connected Cars - Rendu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="bbb5e-186">Réorganisez toutes les visualisations sur cette page comme indiqué dans la figure.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Connected Cars - Visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="bbb5e-188">Vous avez correctement configuré le rapport en temps réel de « Véhicules dans l’opération » hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="bbb5e-189">Vous pouvez passer l’état en temps réel de toocreate hello suivant ou arrêter ici et configurer le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="bbb5e-190">2. Véhicules nécessitant une maintenance</span><span class="sxs-lookup"><span data-stu-id="bbb5e-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="bbb5e-191">Cliquez sur ![ajouter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd un nouveau rapport, renommez-le trop**« Véhicules nécessitant une Maintenance »**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Connected Cars - Véhicules nécessitant une maintenance](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="bbb5e-193">Sélectionnez **vin** champ et modifiez le type de visualisation trop**carte**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="bbb5e-194">![Connected Cars - Visualisation du numéro d’identification du véhicule sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="bbb5e-195">Nous avons un champ nommé « MaintenanceLabel » dans le jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="bbb5e-196">Ce champ peut avoir une valeur de « 0 » ou « 1 ».</span><span class="sxs-lookup"><span data-stu-id="bbb5e-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="bbb5e-197">Elle est définie par le modèle d’Azure Machine Learning hello approvisionné en tant que partie de la solution et intégrés avec le chemin d’accès en temps réel de hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="bbb5e-198">valeur de Hello « 1 » indique un véhicule requiert une maintenance.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="bbb5e-199">tooadd un **niveau Page** filtre pour afficher des données de véhicules, qui nécessitent la maintenance :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="bbb5e-200">Hello de glisser **« MaintenanceLabel »** dans **filtres au niveau de la Page**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="bbb5e-201">![Connected Cars - Filtres au niveau de la page](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="bbb5e-202">Cliquez sur le menu **Filtrage de base** situé en bas du filtre de niveau page MaintenanceLabel.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="bbb5e-203">![Connected Cars - Filtrage de base](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="bbb5e-204">Affectez-lui la valeur filtre trop**« 1 »**  </span><span class="sxs-lookup"><span data-stu-id="bbb5e-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="bbb5e-205">![Connected Cars - Valeur de filtre](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="bbb5e-206">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="bbb5e-207">Sélectionnez **Histogramme groupé** dans la section Visualisations.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="bbb5e-208">![Connected Cars - Visualisation du numéro d’identification du véhicule sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="bbb5e-209">![Connected Cars - Histogramme groupé](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="bbb5e-210">Champ de glisser **modèle** dans **axe** zone, **Vin** trop**valeur** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="bbb5e-211">Triez ensuite la visualisation par **Nombre de vin**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="bbb5e-212">Graphique de modification **titre** trop**« Véhicules nécessitant une maintenance par modèle »**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="bbb5e-213">Faites glisser les champs **vin** dans la zone **Saturation de la couleur** située dans la section **Champs** ![Champs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png)de l’onglet **Visualisation**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="bbb5e-214">![Connected Cars - Saturation des couleurs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="bbb5e-215">Modifiez **Couleurs des données** dans les visualisations à partir de la section **Format**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="bbb5e-216">Définissez **F2C812** comme couleur minimale.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="bbb5e-217">Définissez **FF6300** comme couleur maximale.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="bbb5e-218">![Connected Cars - Changements de couleur](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="bbb5e-219">![Connected Cars - Nouvelles couleurs de visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="bbb5e-220">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="bbb5e-221">Sélectionnez **Histogramme groupé** dans la zone Visualisations, faites glisser le champ **vin** dans la zone **Valeur** et le champ **Ville** dans la zone **Axe**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="bbb5e-222">Triez le graphique par **« Nombre de vin »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="bbb5e-223">Graphique de modification **titre** trop**« Véhicules exigeant une maintenance par ville »** </span><span class="sxs-lookup"><span data-stu-id="bbb5e-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="bbb5e-224">![Connected Cars - Véhicules nécessitant une maintenance par ville](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="bbb5e-225">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="bbb5e-226">Sélectionnez **carte à plusieurs lignes** visualisation à partir des visualisations, faites glisser **modèle** et **vin** dans hello **champs** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="bbb5e-227">![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="bbb5e-228">Réorganisation tous de visualisation de hello, rapport final de hello se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="bbb5e-230">Vous avez correctement configuré le rapport en temps réel de hello « Véhicules nécessitant une Maintenance ».</span><span class="sxs-lookup"><span data-stu-id="bbb5e-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="bbb5e-231">Vous pouvez passer l’état en temps réel de toocreate hello suivant ou arrêter ici et configurer le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="bbb5e-232">3. Statistiques relatives à l’état des véhicules</span><span class="sxs-lookup"><span data-stu-id="bbb5e-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="bbb5e-233">Cliquez sur ![ajouter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nouveau rapport, renommez-le trop**« Statistiques d’intégrité de véhicules »**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="bbb5e-234">Sélectionnez **jauge** visualisation à partir des visualisations, puis faites glisser hello **vitesse** dans **, la valeur minimale, maximale valeur** zones.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="bbb5e-235">![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="bbb5e-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="bbb5e-236">Modifier l’agrégation par défaut de hello de **vitesse** dans **valeur zone** trop**moyenne**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="bbb5e-237">Modifier l’agrégation par défaut de hello de **vitesse** dans **zone de Minimum** trop**Minimum**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="bbb5e-238">Modifier l’agrégation par défaut de hello de **vitesse** dans **zone de Maximum** trop**maximale**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="bbb5e-240">Renommer hello **jauge titre** trop**« Vitesse moyenne »**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Connected Cars - Jauge](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="bbb5e-242">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="bbb5e-243">Vous pouvez également ajouter une **jauge** pour l’**huile moteur moyenne**, le **carburant moyen** et la **température moteur moyenne**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="bbb5e-244">Modifier l’agrégation par défaut de hello des champs de chaque jauge comme indiqué ci-dessus comme suit dans **« Vitesse moyenne »** de jauge.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Connected Cars - Jauges](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="bbb5e-246">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="bbb5e-247">Sélectionnez **courbes et histogramme groupé** à partir des visualisations, puis faites glisser **Ville** dans **axe partagé**, faites glisser **vitesse**, **champs tirepressure et engineoil** dans **les valeurs de colonne** zone, changer le type d’agrégation trop**moyenne**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="bbb5e-248">Hello de glisser **engineTemperature** dans **les valeurs de ligne** zone, modifier le type d’agrégation hello trop**moyenne**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Connected Cars - Champs de visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="bbb5e-250">Graphique de hello modification **titre** trop**« Moyenne vitesse pression des pneus, pétrole de moteur et de température du moteur »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Connected Cars - Champs de visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="bbb5e-252">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="bbb5e-253">Sélectionnez **Treemap** visualisation à partir des visualisations, faites glisser hello **modèle** dans hello **groupe** zone et faites glisser hello champ  **MaintenanceProbability** dans hello **valeurs** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="bbb5e-254">Graphique de hello modification **titre** trop**« Modèles véhicule nécessitant une maintenance »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="bbb5e-256">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="bbb5e-257">Sélectionnez **100 % de graphique à barres empilées** de visualisation, faites glisser hello **Ville** dans hello **axe** zone et faites glisser hello **MaintenanceProbability**, **RecallProbability** champs dans hello **valeur** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="bbb5e-259">Cliquez sur **Format**, sélectionnez **couleurs des données**et ensemble hello **MaintenanceProbability** toohello valeur de couleur **« F2C80F »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="bbb5e-260">Hello de modification **titre** Hello graphique trop**« Probabilité de véhicule Maintenance & rappeler par City »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="bbb5e-262">Cliquez sur Nouvelle visualisation hello zone vide tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="bbb5e-263">Sélectionnez **graphique en aires** de visualisation à partir des visualisations, faites glisser hello **modèle** dans hello **axe** zone et faites glisser hello **engineOil, tirepressure, vitesse et MaintenanceProbability** champs dans hello **valeurs** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="bbb5e-264">Changer le type d’agrégation trop**« Moyenne »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-264">Change their aggregation type too**“Average”**.</span></span> 

![Connected Cars - Modifier le type d’agrégation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="bbb5e-266">Modifier le titre de hello du graphique de hello trop**« Moyenne pétrole de moteur, probabilité pression, la vitesse et la maintenance des pneus par modèle »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="bbb5e-268">Cliquez sur Nouvelle visualisation hello zone vide tooadd :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="bbb5e-269">Dans la section Visualisations, sélectionnez **Nuage de points** .</span><span class="sxs-lookup"><span data-stu-id="bbb5e-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="bbb5e-270">Hello de glisser **modèle** dans hello **détails** et **légende** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="bbb5e-271">Hello de glisser **carburant** dans hello **axe des abscisses** zone, modifiez d’agrégation de hello trop**moyenne**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="bbb5e-272">Faites glisser **engineTemparature** dans **zone de l’axe des y**, changent d’agrégation de hello**moyenne**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="bbb5e-273">Hello de glisser **vin** dans hello **taille** zone.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="bbb5e-275">Graphique de hello modification **titre** trop**« Moyennes de carburant, température moteur par modèle »**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="bbb5e-277">rapport final de Hello ressemble à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-277">hello final report will look like as shown below.</span></span>

![Connected Cars - Rapport final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="bbb5e-279">Code confidentiel des visualisations à partir du tableau de bord en temps réel de la toohello de hello rapports</span><span class="sxs-lookup"><span data-stu-id="bbb5e-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="bbb5e-280">Créer un tableau de bord vide en cliquant sur l’icône plus hello tooDashboards suivant.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="bbb5e-281">Vous pouvez le nommer « Vehicle Telemetry - Tableau de bord d’analyse ».</span><span class="sxs-lookup"><span data-stu-id="bbb5e-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="bbb5e-283">Visualisation de code confidentiel hello de hello au-dessus du tableau de bord toohello rapports.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="bbb5e-285">tableau de bord Hello doit se présenter comme suit lorsque tous les de hello trois rapports sont créés et de hello correspondant visualisations sont épinglées toohello le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="bbb5e-286">Si vous n’avez pas créé tous les rapports de hello, votre tableau de bord peut différer.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="bbb5e-288">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="bbb5e-288">Congratulations!</span></span> <span data-ttu-id="bbb5e-289">Vous venez de créer le tableau de bord en temps réel hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="bbb5e-290">À mesure que vous tooexecute CarEventGenerator.exe et RealtimeDashboardApp.exe, vous devez voir les mises à jour dynamiques sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="bbb5e-291">Il doit prendre hello de toocomplete too15 environ 10 minutes comme suit.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="bbb5e-292">Configuration du tableau de bord de traitement par lots de Power BI</span><span class="sxs-lookup"><span data-stu-id="bbb5e-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="bbb5e-293">Il prend environ deux heures (à partir de l’achèvement réussi de hello du déploiement de hello) pour hello fin tooend lot toofinish l’exécution du pipeline de traitement et de traiter une valeur d’année de données générées.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="bbb5e-294">Par conséquent, attendez hello toofinish avant de procéder aux étapes suivantes de hello de traitement.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="bbb5e-295">**Télécharger le fichier de concepteur hello Power BI**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="bbb5e-296">Un fichier de concepteur préconfiguré Power BI est inclus dans le cadre du déploiement de hello Instructions d’opération manuelle</span><span class="sxs-lookup"><span data-stu-id="bbb5e-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="bbb5e-297">Recherchez 2.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-297">Look for 2.</span></span> <span data-ttu-id="bbb5e-298">Tableau de bord du traitement de lot le programme d’installation Power BI vous pouvez télécharger un modèle de Power BI hello pour le traitement par lots de tableau de bord appelé **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="bbb5e-299">Enregistrez le fichier en local</span><span class="sxs-lookup"><span data-stu-id="bbb5e-299">Save locally</span></span>

<span data-ttu-id="bbb5e-300">**Configurer les rapports Power BI**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="bbb5e-301">Fichier de concepteur hello ouvrir '**ConnectedCarsPbiReport.pbix**' à l’aide de Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="bbb5e-302">Si vous ne pas déjà avez, installez hello Power BI Desktop à partir de [installation de Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="bbb5e-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="bbb5e-303">Cliquez sur hello **modifier les requêtes**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-303">Click hello **Edit Queries**.</span></span>

![Modifier une requête Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="bbb5e-305">Double-cliquez sur hello **Source**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-305">Double-click hello **Source**.</span></span>

![Définir la source Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="bbb5e-307">Mettre à jour la chaîne de connexion de serveur avec le serveur SQL Azure hello qui ont été configuré dans le cadre du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="bbb5e-308">Rechercher dans les Instructions d’opération manuelle hello sous</span><span class="sxs-lookup"><span data-stu-id="bbb5e-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="bbb5e-309">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bbb5e-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="bbb5e-310">Serveur : somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="bbb5e-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="bbb5e-311">Base de données : connectedcar</span><span class="sxs-lookup"><span data-stu-id="bbb5e-311">Database: connectedcar</span></span>
    * <span data-ttu-id="bbb5e-312">Nom d’utilisateur : nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bbb5e-312">Username: username</span></span>
    * <span data-ttu-id="bbb5e-313">Mot de passe : vous pouvez gérer votre mot de passe SQL Server à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="bbb5e-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="bbb5e-314">Laissez la **base de données** en tant que *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-314">Leave **Database** as *connectedcar*.</span></span>

![Définir la base de données Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="bbb5e-316">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-316">Click **OK**.</span></span>
* <span data-ttu-id="bbb5e-317">Vous verrez **informations d’identification Windows** onglet sélectionné par défaut, également le modifier**informations d’identification de base de données** en cliquant sur **base de données** onglet à droite.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="bbb5e-318">Fournir hello **nom d’utilisateur** et **mot de passe** de votre base de données SQL Azure qui a été spécifié pendant l’installation de son déploiement.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Fournir les informations d’identification de la base de données](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="bbb5e-320">Cliquez sur **Connexion**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-320">Click **Connect**</span></span>
* <span data-ttu-id="bbb5e-321">Répétez hello étapes ci-dessus pour chaque hello trois autres requêtes présentes dans le volet droit, puis mettre à jour les détails de connexion de source de données hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="bbb5e-322">Cliquez sur **Fermer et charger**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-322">Click **Close and Load**.</span></span> <span data-ttu-id="bbb5e-323">Jeux de données fichier Power BI Desktop est des tables de base de données Azure tooSQL connecté.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="bbb5e-324">**Fermez** le fichier Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-324">**Close** Power BI Desktop file.</span></span>

![Fermez Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="bbb5e-326">Cliquez sur **enregistrer** bouton les modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="bbb5e-327">Vous avez maintenant configuré tous les rapports hello correspondant toohello chemin de traitement par lots dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="bbb5e-328">Télécharger trop*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="bbb5e-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="bbb5e-329">Accédez toohello portail de web Power BI au http://powerbi.com et à la connexion.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="bbb5e-330">Cliquez sur **Get Data**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="bbb5e-331">Téléchargez hello fichier Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="bbb5e-332">tooupload, cliquez sur **obtenir des données -> fichiers Get -> fichier Local**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="bbb5e-333">Accédez toohello **»**ConnectedCarsPbiReport.pbix**»**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="bbb5e-334">Une fois que le fichier de hello est chargé, vous serez tooyour arrière un espace de travail Power BI.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="bbb5e-335">Un jeu de données, un rapport et un tableau de bord vide sont alors créés.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="bbb5e-336">Code confidentiel graphiques nouveau tableau de bord tooa appelé **tableau de bord véhicule télémétrie Analytique** dans **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="bbb5e-337">Cliquez sur le tableau de bord vide hello créé ci-dessus, puis accédez toohello **rapports** cliquez sur la section hello téléchargé nouveau rapport.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="bbb5e-339">**Remarque hello rapport comporte six pages :**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="bbb5e-340">Page 1 : densité de véhicules</span><span class="sxs-lookup"><span data-stu-id="bbb5e-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="bbb5e-341">Page 2 : intégrité des véhicules en temps réel</span><span class="sxs-lookup"><span data-stu-id="bbb5e-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="bbb5e-342">Page 3 : véhicules utilisés de manière intensive</span><span class="sxs-lookup"><span data-stu-id="bbb5e-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="bbb5e-343">Page 4 : véhicules rappelés</span><span class="sxs-lookup"><span data-stu-id="bbb5e-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="bbb5e-344">Page 5 : véhicules économes en carburant</span><span class="sxs-lookup"><span data-stu-id="bbb5e-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="bbb5e-345">Page 6 : logo de Contoso</span><span class="sxs-lookup"><span data-stu-id="bbb5e-345">Page 6: Contoso Logo</span></span>  

![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="bbb5e-347">**À partir de la Page 3**, épingler des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="bbb5e-348">Nombre de vin</span><span class="sxs-lookup"><span data-stu-id="bbb5e-348">Count of VIN</span></span>  
   ![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="bbb5e-350">Véhicules utilisés de manière intensive par modèle – Graphique en cascade </span><span class="sxs-lookup"><span data-stu-id="bbb5e-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="bbb5e-352">**À partir de la Page 5**, épingler des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="bbb5e-353">Nombre de vin</span><span class="sxs-lookup"><span data-stu-id="bbb5e-353">Count of vin</span></span>    
   ![Vehicle Telemetry - Épingler des graphiques 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="bbb5e-355">Véhicules économes en carburant par modèle : histogramme groupé </span><span class="sxs-lookup"><span data-stu-id="bbb5e-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="bbb5e-357">**À partir de la Page 4**, épingler des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="bbb5e-358">Nombre de vin</span><span class="sxs-lookup"><span data-stu-id="bbb5e-358">Count of vin</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="bbb5e-360">Véhicules rappelés par ville, modèle : Compartimentage </span><span class="sxs-lookup"><span data-stu-id="bbb5e-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="bbb5e-362">**À partir de la Page 6**, épingler des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="bbb5e-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="bbb5e-363">Logo Contoso Motors </span><span class="sxs-lookup"><span data-stu-id="bbb5e-363">Contoso Motors logo</span></span>  
   ![Vehicle Telemetry - Épingler des graphiques 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="bbb5e-365">**Organiser hello le tableau de bord**</span><span class="sxs-lookup"><span data-stu-id="bbb5e-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="bbb5e-366">Accédez toohello le tableau de bord</span><span class="sxs-lookup"><span data-stu-id="bbb5e-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="bbb5e-367">Pointez sur chaque graphique et renommez-la en fonction de hello d’affectation de noms fournis dans l’image du tableau de bord complet hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="bbb5e-368">Également déplacer des graphiques hello autour toolook comme tableau de bord hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Vehicle Telemetry - Organiser le tableau de bord 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="bbb5e-371">Si vous avez créé tous les rapports hello comme indiqué dans ce document, hello final tableau de bord terminé doit ressembler à hello figure suivante.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Vehicle Telemetry - Organiser le tableau de bord 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="bbb5e-373">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="bbb5e-373">Congratulations!</span></span> <span data-ttu-id="bbb5e-374">Vous venez de créer des rapports hello et hello toogain du tableau de bord en temps réel, prédictive et des informations de lot sur l’intégrité du véhicule et du pilotage habituelles.</span><span class="sxs-lookup"><span data-stu-id="bbb5e-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
