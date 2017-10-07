---
title: "solution préconfigurée de maintenance d’aaaPredictive | Documents Microsoft"
description: "Une description de la maintenance prédictive de hello Azure IoT Suite de solution préconfigurée."
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
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="3f03a-103">Présentation de la solution préconfigurée de maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="3f03a-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="3f03a-104">Hello *maintenance prédictive* [solution préconfigurée] [ lnk_preconfigured_solutions] est un des hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] préconfiguré de solutions.</span><span class="sxs-lookup"><span data-stu-id="3f03a-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="3f03a-105">Cette solution intègre la collecte de données télémétriques en temps réel avec un modèle prédictif créé avec [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="3f03a-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="3f03a-106">Avec Azure IoT Suite, vous pouvez rapidement et facilement connectez des ressources d’analyse tooand et analysez la télémétrie en temps réel dans les tableaux de bord et des visualisations.</span><span class="sxs-lookup"><span data-stu-id="3f03a-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="3f03a-107">Dans la solution de maintenance prédictive hello, visualisations et des tableaux de bord hello fournissent avec les nouvelles informations qui vous peuvent de l’efficacité de lecteur et d’améliorer le flux de revenus.</span><span class="sxs-lookup"><span data-stu-id="3f03a-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="3f03a-108">Hello scénario</span><span class="sxs-lookup"><span data-stu-id="3f03a-108">hello Scenario</span></span>

<span data-ttu-id="3f03a-109">Fabrikam est une compagnie aérienne régionale qui s’efforce d’offrir à ses clients une expérience optimale et à des prix compétitifs.</span><span class="sxs-lookup"><span data-stu-id="3f03a-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="3f03a-110">Une des causes de retard des vols est liée à des problèmes de gestion, et la maintenance des moteurs d'avion est particulièrement complexe.</span><span class="sxs-lookup"><span data-stu-id="3f03a-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="3f03a-111">Fabrikam doit éviter de défaillance du moteur pendant un vol à tout prix, pour qu’il examine ses moteurs régulièrement et planifie en fonction de tooa plan de maintenance.</span><span class="sxs-lookup"><span data-stu-id="3f03a-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="3f03a-112">Toutefois, avion moteurs ne portez toujours hello identiques.</span><span class="sxs-lookup"><span data-stu-id="3f03a-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="3f03a-113">Et certaines opérations de maintenance inutiles sont effectuées sur les moteurs.</span><span class="sxs-lookup"><span data-stu-id="3f03a-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="3f03a-114">Plus important encore, les problèmes clouent les appareils au sol jusqu'à ce que l'opération de maintenance soit terminée.</span><span class="sxs-lookup"><span data-stu-id="3f03a-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="3f03a-115">Si un appareil situé à un emplacement où hello techniciens droit ou pièces de rechange ne sont pas disponibles, ces problèmes peuvent être particulièrement coûteux.</span><span class="sxs-lookup"><span data-stu-id="3f03a-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="3f03a-116">moteurs Hello d’avion de Fabrikam sont instrumentés avec capteurs qui analyse les conditions du moteur au cours du vol.</span><span class="sxs-lookup"><span data-stu-id="3f03a-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="3f03a-117">Fabrikam utilise hello maintenance prédictive solution toocollect hello capteur données collectées au cours du vol de hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="3f03a-118">Après avoir années accumuler du moteur opérationnel et données de défaillance, les chercheurs de données de Fabrikam ont modélisée un Bonjour toopredict de façon restant cycle de vie (RUL) un moteur d’avion.</span><span class="sxs-lookup"><span data-stu-id="3f03a-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="3f03a-119">modèle de Hello utilise une corrélation entre les données à partir de quatre des capteurs de moteur hello et usure moteur qui entraîne l’échec de tooeventual.</span><span class="sxs-lookup"><span data-stu-id="3f03a-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="3f03a-120">Fabrikam interrompre la sécurité de tooensure tooperform contrôle régulier, elle peut désormais utiliser hello modèles toocompute hello RUL pour chaque moteur après chaque vol.</span><span class="sxs-lookup"><span data-stu-id="3f03a-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="3f03a-121">modèle de Hello utilise télémétrie hello collectée à partir de moteurs de hello au cours du vol de hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="3f03a-122">Fabrikam peut désormais anticiper les futurs points de défaillance, la planification de la maintenance et les réparations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="3f03a-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="3f03a-123">modèle de solution Hello utilise des données d’usure de moteur réel.</span><span class="sxs-lookup"><span data-stu-id="3f03a-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="3f03a-124">La prédiction de point de hello lors de la maintenance n’est requise, Fabrikam peut optimiser ses coûts de tooreduce d’opérations.</span><span class="sxs-lookup"><span data-stu-id="3f03a-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="3f03a-125">Les coordinateurs de maintenance collaborent avec les planificateurs pour :</span><span class="sxs-lookup"><span data-stu-id="3f03a-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="3f03a-126">Plan de maintenance toocoincide avec un appareil de l’arrêt à un emplacement particulier.</span><span class="sxs-lookup"><span data-stu-id="3f03a-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="3f03a-127">Assurez-vous que suffisamment de temps est disponible pour toobe d’avion hello hors service sans provoquer l’interruption de la planification.</span><span class="sxs-lookup"><span data-stu-id="3f03a-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="3f03a-128">tooensure de techniciens tooschedule que les appareils sont traitées efficacement sans temps d’attente.</span><span class="sxs-lookup"><span data-stu-id="3f03a-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="3f03a-129">Les responsables du contrôle des stocks reçoivent des plans de maintenance qui les aident à optimiser le processus de commande et le stock de pièces de rechange.</span><span class="sxs-lookup"><span data-stu-id="3f03a-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="3f03a-130">Ces activités activer l’heure de Fabrikam toominimize avion sol et réduisent les coûts d’exploitation tout en assurant la sécurité hello de passagers et personnel.</span><span class="sxs-lookup"><span data-stu-id="3f03a-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="3f03a-131">toounderstand comment [Azure IoT Suite] [ lnk_iot_suite] fournit aux clients les fonctionnalités de hello besoin potentiel de hello toorealize de maintenance prédictive, passez en revue cette [graphisme d’information] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="3f03a-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="3f03a-132">La création de la solution de maintenance prédictive hello</span><span class="sxs-lookup"><span data-stu-id="3f03a-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="3f03a-133">solution de Hello utilise un modèle de disponibles en Azure Machine Learning existant comme un modèle tooshow ces fonctionnalités à partir de télémétrie recueillie via les services IoT Suite de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3f03a-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="3f03a-134">Microsoft a créé un [modèle de régression] [ lnk_regression_model] un moteur d’avion en fonction des données disponibles publiquement<sup>\[1\]</sup>et pas à pas conseils sur la toouse hello modèle.</span><span class="sxs-lookup"><span data-stu-id="3f03a-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="3f03a-135">Hello solution de maintenance prédictive Azure IoT utilise un modèle de régression hello créé à partir de ce modèle.</span><span class="sxs-lookup"><span data-stu-id="3f03a-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="3f03a-136">modèle de Hello est déployé dans votre abonnement Azure et exposée via une API générée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="3f03a-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="3f03a-137">solution de Hello inclut un sous-ensemble de hello représentant 4 (de 100 total) des données de test moteurs et flux de données de capteur hello 4 (de total de 21).</span><span class="sxs-lookup"><span data-stu-id="3f03a-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="3f03a-138">Ces données sont suffisante tooprovide un résultat exact du modèle formé de hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="3f03a-139">*\[1\] A. Saxena and K. Goebel (2008). « Turbofan Engine Degradation Simulation Data Set », NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="3f03a-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="3f03a-140">Prise en main de la maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="3f03a-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="3f03a-141">Ce didacticiel vous montre comment tooprovision hello solution de maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="3f03a-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="3f03a-142">Il vous guide également dans les fonctionnalités de base hello de solution de maintenance prédictive hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="3f03a-143">Vous pouvez accéder à la plupart de ces fonctionnalités via hello solution du tableau de bord qui déploie en même temps que la solution de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="3f03a-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="3f03a-144">toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="3f03a-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="3f03a-145">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3f03a-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3f03a-146">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="3f03a-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="3f03a-147">Ouvrez une session trop[azureiotsuite.com] [ lnk-azureiotsuite] à l’aide de votre Azure des informations d’identification de compte, puis cliquez sur  **+**  toocreate une solution.</span><span class="sxs-lookup"><span data-stu-id="3f03a-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="3f03a-148">Cliquez sur **sélectionnez** hello **maintenance prédictive** vignette.</span><span class="sxs-lookup"><span data-stu-id="3f03a-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="3f03a-149">Entrez un **Nom de solution** pour votre solution préconfigurée de maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="3f03a-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="3f03a-150">Sélectionnez hello **région** et **abonnement** vous souhaitez toouse tooprovision hello solution.</span><span class="sxs-lookup"><span data-stu-id="3f03a-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="3f03a-151">Cliquez sur **créer une Solution** hello toobegin processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="3f03a-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="3f03a-152">Ce processus dure généralement plusieurs minutes toorun.</span><span class="sxs-lookup"><span data-stu-id="3f03a-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="3f03a-153">Attendez que hello toocomplete du processus de configuration</span><span class="sxs-lookup"><span data-stu-id="3f03a-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="3f03a-154">Cliquez sur la vignette hello pour votre solution avec **Provisioning** état.</span><span class="sxs-lookup"><span data-stu-id="3f03a-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="3f03a-155">Hello d’avis **les États de configuration** comme des services Azure sont déployés dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3f03a-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="3f03a-156">Une fois la configuration terminée, modifications d’état hello trop**prêt**.</span><span class="sxs-lookup"><span data-stu-id="3f03a-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="3f03a-157">Cliquez sur Détails de hello toosee hello vignette de votre solution dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="3f03a-158">Dans ce volet, vous pouvez lancer hello solution tableau de bord et des accès hello apprentissage espace de travail.</span><span class="sxs-lookup"><span data-stu-id="3f03a-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="3f03a-159">Si vous rencontrez des problèmes de déploiement de solution de hello préconfiguré, passez en revue [autorisations sur le site de azureiotsuite.com hello] [ lnk-permissions] et hello [FAQ] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="3f03a-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="3f03a-160">Si les problèmes de hello persistent, créer un ticket de service sur hello [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="3f03a-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="3f03a-161">Existe-t-il des détails que toosee souhaitées et qui ne sont pas répertoriés pour votre solution ?</span><span class="sxs-lookup"><span data-stu-id="3f03a-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="3f03a-162">Faites-nous part de vos suggestions concernant les fonctionnalités sur [UserVoice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="3f03a-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="3f03a-163">Afficher la solution hello</span><span class="sxs-lookup"><span data-stu-id="3f03a-163">View hello solution</span></span>

<span data-ttu-id="3f03a-164">Cette section vous guide tout au long de la solution de hello l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3f03a-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="3f03a-165">Tableau de bord de maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="3f03a-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="3f03a-166">Cette page dans l’application web de hello utilise les contrôles de PowerBI JavaScript (voir hello [référentiel de PowerBI-visuals][lnk-powerbi]) toovisualize :</span><span class="sxs-lookup"><span data-stu-id="3f03a-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="3f03a-167">Hello les données de sortie de tâches de flux de données Analytique hello dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="3f03a-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="3f03a-168">Hello RUL et cycle de nombre par le moteur d’avion.</span><span class="sxs-lookup"><span data-stu-id="3f03a-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="3f03a-169">En observant comportement hello de solution de cloud hello</span><span class="sxs-lookup"><span data-stu-id="3f03a-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="3f03a-170">Dans l’hello portail Azure, accédez de groupe de ressources toohello avec le nom de la solution hello choisis tooview vos ressources configurées.</span><span class="sxs-lookup"><span data-stu-id="3f03a-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="3f03a-171">Lorsque vous configurez la solution de hello préconfiguré, vous recevez un message électronique contenant un espace de travail de lien toohello Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3f03a-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="3f03a-172">Vous pouvez également naviguer toohello espace de travail Machine Learning à partir de hello [azureiotsuite.com] [ lnk-azureiotsuite] page de votre solution approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="3f03a-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="3f03a-173">Une mosaïque est disponible sur cette page lors de la solution de hello est Bonjour **prêt** état.</span><span class="sxs-lookup"><span data-stu-id="3f03a-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="3f03a-174">Dans le portail de solution hello, vous pouvez voir que cet exemple hello est doté d’appareils de deux toorepresent quatre périphériques simulé avec deux moteurs par avion, chacun avec quatre capteurs.</span><span class="sxs-lookup"><span data-stu-id="3f03a-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="3f03a-175">Lorsque vous accédez d’abord portal de solution toohello, la simulation hello est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="3f03a-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="3f03a-176">Cliquez sur **démarrer simulation** toobegin la simulation hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="3f03a-177">Hello historique de capteur, RUL, Cycles et RUL historique remplir le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="3f03a-178">Lorsque RUL est inférieur à 160 (un seuil arbitraire choisi à des fins de démonstration), portail de solution hello affiche un avertissement symbole suivant toohello RUL afficher.</span><span class="sxs-lookup"><span data-stu-id="3f03a-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="3f03a-179">portail de solution Hello met également en surbrillance le moteur d’avion hello en jaune.</span><span class="sxs-lookup"><span data-stu-id="3f03a-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="3f03a-180">Notez comment les valeurs hello RUL ont une tendance vers le bas générale globale, mais ont tendance toobounce haut et bas.</span><span class="sxs-lookup"><span data-stu-id="3f03a-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="3f03a-181">Ce comportement les résultats de différentes longueurs de cycle hello et la précision du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="3f03a-182">la simulation complète Hello prend environ 35 minutes toocomplete 148 cycles.</span><span class="sxs-lookup"><span data-stu-id="3f03a-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="3f03a-183">seuil RUL 160 Hello est remplie pour hello première fois à environ 5 minutes et les deux moteurs atteint le seuil de hello à environ 8 minutes.</span><span class="sxs-lookup"><span data-stu-id="3f03a-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="3f03a-184">simulation de Hello s’exécute via un jeu de données complet hello pour les cycles de 148 et règle sur les valeurs finales RUL et cycle.</span><span class="sxs-lookup"><span data-stu-id="3f03a-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="3f03a-185">Vous pouvez arrêter la simulation hello à n’importe quel point, mais en cliquant sur **démarrer la Simulation** relectures hello simulation du début de hello du jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f03a-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f03a-186">Next steps</span></span>

<span data-ttu-id="3f03a-187">toolearn plus en détail comment Azure IoT permet des scénarios de maintenance prédictive, lire [capturer la valeur à partir de hello Internet of Things][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="3f03a-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="3f03a-188">Prendre un [procédure pas à pas] [ lnk-predictive-walkthrough] de solution de maintenance prédictive hello.</span><span class="sxs-lookup"><span data-stu-id="3f03a-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="3f03a-189">Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :</span><span class="sxs-lookup"><span data-stu-id="3f03a-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="3f03a-190">[Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="3f03a-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="3f03a-191">[IoT hello d’arrière-plan la sécurité][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="3f03a-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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