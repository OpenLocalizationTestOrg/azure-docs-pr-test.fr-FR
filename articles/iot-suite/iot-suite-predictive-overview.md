---
title: "Solution préconfigurée de maintenance prédictive | Microsoft Docs"
description: "Description de la solution préconfigurée de maintenance prédictive Azure IoT Suite."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="47fd0-103">Présentation de la solution préconfigurée de maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="47fd0-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="47fd0-104">La *solution préconfigurée* de [maintenance prédictive][lnk_preconfigured_solutions] est l’une des solutions préconfigurées incluses dans [Microsoft Azure IoT Suite][lnk_iot_suite].</span><span class="sxs-lookup"><span data-stu-id="47fd0-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="47fd0-105">Cette solution intègre la collecte de données télémétriques en temps réel avec un modèle prédictif créé avec [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="47fd0-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="47fd0-106">Avec Azure IoT Suite, vous pouvez rapidement et facilement accéder aux ressources, les surveiller et analyser des données de télémétrie en temps réels dans des tableaux de bords et des visualisations.</span><span class="sxs-lookup"><span data-stu-id="47fd0-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="47fd0-107">Dans cette solution de maintenance prédictive, les tableaux de bord ainsi que les visualisations vous fournissent de nouvelles informations pertinentes vous permettant d’accroître votre efficacité et vos flux de revenus.</span><span class="sxs-lookup"><span data-stu-id="47fd0-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="47fd0-108">Le scénario</span><span class="sxs-lookup"><span data-stu-id="47fd0-108">The Scenario</span></span>

<span data-ttu-id="47fd0-109">Fabrikam est une compagnie aérienne régionale qui s’efforce d’offrir à ses clients une expérience optimale et à des prix compétitifs.</span><span class="sxs-lookup"><span data-stu-id="47fd0-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="47fd0-110">Une des causes de retard des vols est liée à des problèmes de gestion, et la maintenance des moteurs d'avion est particulièrement complexe.</span><span class="sxs-lookup"><span data-stu-id="47fd0-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="47fd0-111">Une panne de moteur en plein vol devant être évitée à tout prix, Fabrikam inspecte ses moteurs régulièrement et suit un programme de maintenance planifiée.</span><span class="sxs-lookup"><span data-stu-id="47fd0-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="47fd0-112">Mais les moteurs d’avion ne vieillissent pas tous de la même manière.</span><span class="sxs-lookup"><span data-stu-id="47fd0-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="47fd0-113">Et certaines opérations de maintenance inutiles sont effectuées sur les moteurs.</span><span class="sxs-lookup"><span data-stu-id="47fd0-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="47fd0-114">Plus important encore, les problèmes clouent les appareils au sol jusqu'à ce que l'opération de maintenance soit terminée.</span><span class="sxs-lookup"><span data-stu-id="47fd0-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="47fd0-115">Si un appareil est immobilisé sur un site qui ne dispose pas des techniciens qualifiés ni des pièces de rechange nécessaires, ces problèmes peuvent s’avérer particulièrement coûteux.</span><span class="sxs-lookup"><span data-stu-id="47fd0-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="47fd0-116">Les appareils de Fabrikam sont équipés de capteurs qui analysent les paramètres du moteur pendant le vol.</span><span class="sxs-lookup"><span data-stu-id="47fd0-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="47fd0-117">Fabrikam utilise la solution de maintenance prédictive pour récupérer les données des capteurs collectées pendant le vol.</span><span class="sxs-lookup"><span data-stu-id="47fd0-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="47fd0-118">Après de longues années passées à analyser les données liées au fonctionnement et aux pannes des moteurs, les spécialistes de Fabrikam ont modélisé une solution capable de prédire la durée de vie restante ou RUL (Remaining Useful Life) d’un moteur d'avion.</span><span class="sxs-lookup"><span data-stu-id="47fd0-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="47fd0-119">Le modèle se sert d’une corrélation entre les données de quatre des capteurs moteur et l'usure du moteur conduisant à une panne.</span><span class="sxs-lookup"><span data-stu-id="47fd0-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="47fd0-120">Tandis que Fabrikam continue à effectuer des inspections régulières pour garantir la sécurité, l’entreprise peut maintenant utiliser les modèles pour calculer la durée de vie utile restante de chaque moteur après chaque vol.</span><span class="sxs-lookup"><span data-stu-id="47fd0-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="47fd0-121">Le modèle utilise les données télémétriques collectées par les moteurs pendant le vol.</span><span class="sxs-lookup"><span data-stu-id="47fd0-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="47fd0-122">Fabrikam peut désormais anticiper les futurs points de défaillance, la planification de la maintenance et les réparations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="47fd0-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="47fd0-123">Le modèle de solution utilise les données réelles d’usure du moteur.</span><span class="sxs-lookup"><span data-stu-id="47fd0-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="47fd0-124">En prédisant le moment où une maintenance est requise, Fabrikam peut optimiser ses opérations et réduire ainsi ses coûts.</span><span class="sxs-lookup"><span data-stu-id="47fd0-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="47fd0-125">Les coordinateurs de maintenance collaborent avec les planificateurs pour :</span><span class="sxs-lookup"><span data-stu-id="47fd0-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="47fd0-126">Prévoir une maintenance lorsqu’un appareil est au sol sur un site donné.</span><span class="sxs-lookup"><span data-stu-id="47fd0-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="47fd0-127">Garantir un délai suffisant pour que la mise hors service de l’avion ne perturbe pas la planification.</span><span class="sxs-lookup"><span data-stu-id="47fd0-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="47fd0-128">pour planifier le travail des techniciens en veillant à ce que les appareils sont inspectés et réparés sans délai.</span><span class="sxs-lookup"><span data-stu-id="47fd0-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="47fd0-129">Les responsables du contrôle des stocks reçoivent des plans de maintenance qui les aident à optimiser le processus de commande et le stock de pièces de rechange.</span><span class="sxs-lookup"><span data-stu-id="47fd0-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="47fd0-130">Ces activités permettent à Fabrikam de minimiser le temps d’immobilisation des appareils et de réduire les coûts d’exploitation tout en garantissant la sécurité des passagers et de l’équipage.</span><span class="sxs-lookup"><span data-stu-id="47fd0-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="47fd0-131">Pour comprendre comment les fonctionnalités [d’Azure IoT Suite][lnk_iot_suite] permettent aux clients d’exploiter tout le potentiel de la maintenance prédictive, reportez-vous à cette [infographie][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="47fd0-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="47fd0-132">Comment la solution de gestion prédictive est générée</span><span class="sxs-lookup"><span data-stu-id="47fd0-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="47fd0-133">La solution utilise un modèle Microsoft Azure Machine Learning existant pour afficher ces fonctionnalités en s’appuyant sur les données télémétriques de l’appareil recueillies via les services IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="47fd0-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="47fd0-134">Microsoft a créé un [modèle de régression][lnk_regression_model] d’un moteur d’avion basé sur un modèle complet disponible publiquement<sup>\[1\]</sup> et des instructions d’utilisation détaillées.</span><span class="sxs-lookup"><span data-stu-id="47fd0-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="47fd0-135">La solution de maintenance prédictive Azure IoT utilise le modèle de régression créé à partir de ce modèle.</span><span class="sxs-lookup"><span data-stu-id="47fd0-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="47fd0-136">Le modèle est déployé dans votre abonnement Azure et exposé via une API générée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="47fd0-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="47fd0-137">La solution inclut un sous-ensemble des données de tests représentant 4 (sur un total 100) moteurs et 4 (sur un total 21) flux de données de capteurs.</span><span class="sxs-lookup"><span data-stu-id="47fd0-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="47fd0-138">Ces données sont suffisantes pour fournir un résultat exact du modèle formé.</span><span class="sxs-lookup"><span data-stu-id="47fd0-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="47fd0-139">*\[1\] A. Saxena and K. Goebel (2008). « Turbofan Engine Degradation Simulation Data Set », NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="47fd0-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="47fd0-140">Prise en main de la maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="47fd0-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="47fd0-141">Ce didacticiel vous montre comment configurer la solution de maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="47fd0-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="47fd0-142">Il présente également les fonctionnalités de base de la solution de maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="47fd0-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="47fd0-143">Vous pouvez accéder à la plupart de ces fonctionnalités via le tableau de bord de solution déployé avec la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="47fd0-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="47fd0-144">Pour suivre ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="47fd0-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="47fd0-145">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="47fd0-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="47fd0-146">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="47fd0-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="47fd0-147">Connectez-vous à [azureiotsuite.com][lnk-azureiotsuite] à l’aide des informations d’identification de votre compte Azure, puis cliquez sur **+** pour créer une solution.</span><span class="sxs-lookup"><span data-stu-id="47fd0-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="47fd0-148">Cliquez sur **Sélectionner** et choisissez la vignette **Maintenance prédictive**.</span><span class="sxs-lookup"><span data-stu-id="47fd0-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="47fd0-149">Entrez un **Nom de solution** pour votre solution préconfigurée de maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="47fd0-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="47fd0-150">Sélectionnez la **région** et **l’abonnement** à utiliser pour configurer la solution.</span><span class="sxs-lookup"><span data-stu-id="47fd0-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="47fd0-151">Cliquez sur **Créer une solution** pour commencer le processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="47fd0-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="47fd0-152">L’exécution de ce processus prend généralement plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="47fd0-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="47fd0-153">Attendre la fin du processus d’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="47fd0-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="47fd0-154">Cliquez sur la vignette de votre solution présentant l’état **Approvisionnement** .</span><span class="sxs-lookup"><span data-stu-id="47fd0-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="47fd0-155">Notez les **états d’approvisionnement** à mesure que les services Azure sont déployés dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="47fd0-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="47fd0-156">Une fois l’approvisionnement terminé, l’état prend la valeur **Prêt**.</span><span class="sxs-lookup"><span data-stu-id="47fd0-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="47fd0-157">Cliquez sur la vignette pour visualiser les détails de votre solution dans le volet droit.</span><span class="sxs-lookup"><span data-stu-id="47fd0-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="47fd0-158">Dans ce volet, vous pouvez démarrer le tableau de bord de la solution et accéder à l’espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="47fd0-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="47fd0-159">Si vous rencontrez des problèmes lors du déploiement de la solution préconfigurée, consultez les articles [Autorisations sur le site azureiotsuite.com][lnk-permissions] et [Forum Aux Questions][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="47fd0-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="47fd0-160">Si les problèmes persistent, créez un ticket de service sur le [Portail][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="47fd0-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="47fd0-161">Certains détails de votre solution semblent-ils faire défaut ?</span><span class="sxs-lookup"><span data-stu-id="47fd0-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="47fd0-162">Faites-nous part de vos suggestions concernant les fonctionnalités sur [UserVoice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="47fd0-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="47fd0-163">Afficher la solution</span><span class="sxs-lookup"><span data-stu-id="47fd0-163">View the solution</span></span>

<span data-ttu-id="47fd0-164">Cette section vous guide à travers l’utilisation de l’interface utilisateur de la solution.</span><span class="sxs-lookup"><span data-stu-id="47fd0-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="47fd0-165">Tableau de bord de maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="47fd0-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="47fd0-166">Cette page de l’application web utilise des contrôles Power BI JavaScript (consultez [Référentiel d’éléments visuels Power BI][lnk-powerbi]) pour visualiser :</span><span class="sxs-lookup"><span data-stu-id="47fd0-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="47fd0-167">Les données de sortie des tâches Stream Analytics dans le Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="47fd0-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="47fd0-168">La durée de vie utile restante et le nombre de cycles d’un moteur d’avion.</span><span class="sxs-lookup"><span data-stu-id="47fd0-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="47fd0-169">Observer le comportement de la solution cloud</span><span class="sxs-lookup"><span data-stu-id="47fd0-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="47fd0-170">Dans le portail Azure, accédez au groupe de ressources portant le nom de solution que vous avez choisi, pour afficher vos ressources configurées.</span><span class="sxs-lookup"><span data-stu-id="47fd0-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="47fd0-171">Lorsque vous approvisionnez la solution préconfigurée, vous recevez un e-mail contenant un lien vers l’espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="47fd0-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="47fd0-172">Vous pouvez également accéder à l’espace de travail Machine Learning à partir de la page [azureiotsuite.com][lnk-azureiotsuite] de votre solution configurée.</span><span class="sxs-lookup"><span data-stu-id="47fd0-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="47fd0-173">Une vignette est disponible sur cette page lorsque le statut de la solution est **Prêt**.</span><span class="sxs-lookup"><span data-stu-id="47fd0-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="47fd0-174">Dans le portail de la solution, vous pouvez voir que l’exemple est configuré avec quatre appareils simulés, correspondant à deux avions avec deux moteurs chacun et quatre capteurs par moteur.</span><span class="sxs-lookup"><span data-stu-id="47fd0-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="47fd0-175">Lorsque vous accédez au portail de la solution pour la première fois, la simulation est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="47fd0-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="47fd0-176">Cliquez sur **Démarrer la simulation** pour commencer la simulation.</span><span class="sxs-lookup"><span data-stu-id="47fd0-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="47fd0-177">L’historique, les cycles et la durée de vie utile restante du capteur, ainsi que l’historique de durée de vie restante sont renseignés dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="47fd0-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="47fd0-178">Lorsque la durée de vie utile restante est inférieure à 160 (seuil arbitraire choisi pour les besoins de la démonstration), le portail de la solution affiche un symbole d’avertissement en regard de la valeur correspondante.</span><span class="sxs-lookup"><span data-stu-id="47fd0-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="47fd0-179">Le portail de la solution colore également le moteur d’avion en jaune.</span><span class="sxs-lookup"><span data-stu-id="47fd0-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="47fd0-180">Vous remarquerez que les valeurs de durée de vie utile restante tendent globalement à diminuer, mais avec des rebonds à la hausse ou à la baisse.</span><span class="sxs-lookup"><span data-stu-id="47fd0-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="47fd0-181">Ce phénomène provient de la variabilité de la durée des cycles et de la précision du modèle.</span><span class="sxs-lookup"><span data-stu-id="47fd0-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="47fd0-182">La simulation complète prend environ 35 minutes pour effectuer 148 cycles.</span><span class="sxs-lookup"><span data-stu-id="47fd0-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="47fd0-183">Le seuil de durée de vie utile restante de 160 est atteint pour la première fois à environ 5 minutes, et les deux moteurs atteignent le seuil à environ 8 minutes.</span><span class="sxs-lookup"><span data-stu-id="47fd0-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="47fd0-184">La simulation s’exécute sur le jeu de données complet pour les 148 cycles et se règle sur les valeurs finales de durée de vie utile restante et de cycles.</span><span class="sxs-lookup"><span data-stu-id="47fd0-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="47fd0-185">Vous pouvez arrêter la simulation à tout moment. L’option **Démarrer la simulation** réexécute la simulation à partir du début du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="47fd0-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47fd0-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47fd0-186">Next steps</span></span>

<span data-ttu-id="47fd0-187">Pour en savoir plus sur la gestion de scénarios de gestion prédictive avec Azure IoT, consultez [Saisir la valeur de l'Internet des objets][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="47fd0-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="47fd0-188">[Examinez pas à pas][lnk-predictive-walkthrough] la solution de maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="47fd0-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="47fd0-189">Vous pouvez également explorer certaines des autres fonctionnalités et capacités des solutions préconfigurées IoT Suite :</span><span class="sxs-lookup"><span data-stu-id="47fd0-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="47fd0-190">[Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="47fd0-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="47fd0-191">[Sécurisation de l’Internet des objets de bout en bout][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="47fd0-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/