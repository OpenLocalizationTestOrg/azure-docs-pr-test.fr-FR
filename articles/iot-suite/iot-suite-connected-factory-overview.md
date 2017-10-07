---
title: "aaaAzure IoT Suite connecté vue d’ensemble de la fabrique | Documents Microsoft"
description: "Obtenir une description de hello Azure IoT Suite connecté solution de fabrique préconfiguré."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="47732-103">Prise en main hello connecté fabrique préconfiguré solution</span><span class="sxs-lookup"><span data-stu-id="47732-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="47732-104">Azure IoT Suite [préconfiguré solutions] [ lnk-preconfigured-solutions] combiner plusieurs Azure IoT services toodeliver bout en bout pour les solutions qui implémentent des scénarios d’entreprise IoT.</span><span class="sxs-lookup"><span data-stu-id="47732-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="47732-105">Hello *fabrique connecté* solution préconfigurée connecte tooand surveille vos appareils industriels.</span><span class="sxs-lookup"><span data-stu-id="47732-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="47732-106">Vous pouvez utiliser des flux de hello hello solution tooanalyze de données à partir de vos appareils et la productivité opérationnelle de toodrive et la rentabilité.</span><span class="sxs-lookup"><span data-stu-id="47732-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="47732-107">Ce didacticiel vous montre comment tooprovision hello connectées fabrique solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="47732-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="47732-108">Il vous guide également dans les fonctionnalités de base hello de solution de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="47732-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="47732-109">Vous pouvez accéder à la plupart de ces fonctionnalités à partir de la solution de hello *tableau de bord* qui déploie dans le cadre de la solution de hello préconfiguré :</span><span class="sxs-lookup"><span data-stu-id="47732-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![tableau de bord de solution préconfigurée d’usine connectée][img-cf-home]

<span data-ttu-id="47732-111">toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="47732-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="47732-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="47732-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="47732-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="47732-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="47732-114">Solution de hello de disposition</span><span class="sxs-lookup"><span data-stu-id="47732-114">Provision hello solution</span></span>

1. <span data-ttu-id="47732-115">Ouvrez une session sur tooazureiotsuite.com à l’aide de vos informations d’identification de compte Azure, puis cliquez sur «**+**« toocreate une solution.</span><span class="sxs-lookup"><span data-stu-id="47732-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="47732-116">Cliquez sur **sélectionnez** sur hello **fabrique connecté** vignette.</span><span class="sxs-lookup"><span data-stu-id="47732-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="47732-117">Entrez un **Nom de solution** pour votre solution préconfigurée d’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="47732-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="47732-118">Sélectionnez hello **abonnement** et **région** vous souhaitez toouse tooprovision hello solution.</span><span class="sxs-lookup"><span data-stu-id="47732-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="47732-119">Cliquez sur **créer une Solution** hello toobegin processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="47732-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="47732-120">Ce processus dure généralement plusieurs minutes toorun.</span><span class="sxs-lookup"><span data-stu-id="47732-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="47732-121">Alors que vous attendez hello toocomplete du processus de configuration</span><span class="sxs-lookup"><span data-stu-id="47732-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="47732-122">Cliquez sur la vignette hello pour votre solution avec **Provisioning** état.</span><span class="sxs-lookup"><span data-stu-id="47732-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="47732-123">Hello d’avis **les États de configuration** comme des services Azure sont déployés dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="47732-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="47732-124">Une fois la configuration terminée, modifications d’état hello trop**prêt**.</span><span class="sxs-lookup"><span data-stu-id="47732-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="47732-125">Cliquez sur Détails de hello toosee hello vignette de votre solution dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="47732-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="47732-126">Si vous rencontrez des problèmes de déploiement de solution de hello préconfiguré, passez en revue [autorisations sur le site de azureiotsuite.com hello] [ lnk-permissions] et hello [connecté fabrique FAQ](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="47732-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="47732-127">Si les problèmes de hello persistent, créer un ticket de service sur hello [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="47732-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="47732-128">Existe-t-il des détails que toosee souhaitées et qui ne sont pas répertoriés pour votre solution ?</span><span class="sxs-lookup"><span data-stu-id="47732-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="47732-129">Faites-nous part de vos suggestions concernant les fonctionnalités sur [UserVoice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="47732-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="47732-130">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="47732-130">Scenario overview</span></span>

<span data-ttu-id="47732-131">Lorsque vous déployez hello connecté solution préconfigurée de fabrique, il est préremplie avec les ressources qui vous permettent de toostep un scénario industrielle commune.</span><span class="sxs-lookup"><span data-stu-id="47732-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="47732-132">Dans ce scénario, plusieurs fabriques connecté le rapport des solutions toohello toocompute requis de valeurs de données de hello l’efficacité globale équipement (OEE) et les indicateurs de performance clés (KPI).</span><span class="sxs-lookup"><span data-stu-id="47732-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="47732-133">Hello sections suivantes vous indiquent comment procéder pour :</span><span class="sxs-lookup"><span data-stu-id="47732-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="47732-134">Surveiller des valeurs d’usine, de lignes de production, OEE de poste et KPI</span><span class="sxs-lookup"><span data-stu-id="47732-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="47732-135">Analyser les données de télémétrie hello générées à partir de ces appareils à l’aide de la série de temps Azure Insights</span><span class="sxs-lookup"><span data-stu-id="47732-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="47732-136">Agir sur les problèmes de toofix d’alertes</span><span class="sxs-lookup"><span data-stu-id="47732-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="47732-137">Une fonctionnalité clé de ce scénario est que vous pouvez effectuer toutes ces actions à distance à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="47732-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="47732-138">Vous n’avez pas besoin d’appareils de toohello d’accès physique.</span><span class="sxs-lookup"><span data-stu-id="47732-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="47732-139">Tableau de bord View hello solution</span><span class="sxs-lookup"><span data-stu-id="47732-139">View hello solution dashboard</span></span>

<span data-ttu-id="47732-140">tableau de bord Hello solution vous permet de solution de hello déployé toomanage.</span><span class="sxs-lookup"><span data-stu-id="47732-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="47732-141">Il s’agit d’une représentation hiérarchique d’une configuration d’usine globale.</span><span class="sxs-lookup"><span data-stu-id="47732-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="47732-142">Par exemple, vous pouvez afficher l’OEE et les KPI, publier de nouveaux nœuds pour la télémétrie et les alertes d’action.</span><span class="sxs-lookup"><span data-stu-id="47732-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="47732-143">Lorsque l’approvisionnement hello est terminé et vignette hello pour votre solution préconfigurée indique **prêt**, choisissez **lancer** tooopen votre portail de solution fabrique connecté dans un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="47732-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Lancer la solution de hello préconfiguré][img-launch-solution]

1. <span data-ttu-id="47732-145">Par défaut, portail de solution hello affiche hello *tableau de bord*.</span><span class="sxs-lookup"><span data-stu-id="47732-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="47732-146">zones de tooother toonavigate du portail de hello, utiliser les menus hello sur la partie gauche de la page de hello hello.</span><span class="sxs-lookup"><span data-stu-id="47732-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Tableau de bord de solution préconfigurée d’usine connectée][cf-img-menu]

<span data-ttu-id="47732-148">tableau de bord Hello affiche hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="47732-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="47732-149">A **liste de paramètres d’usine** panneau qui affiche l’état de hello, l’emplacement et configuration de production actuelle dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="47732-150">Lorsque vous exécutez la solution de hello pour la première fois, il existe un nombre de périphériques simulés.</span><span class="sxs-lookup"><span data-stu-id="47732-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="47732-151">simulation de ligne de production Hello est composée de trois serveurs OPC UA réels par ligne de production qui effectuent des tâches simulés et partagent des données.</span><span class="sxs-lookup"><span data-stu-id="47732-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="47732-152">Pour plus d’informations sur OPC UA, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="47732-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="47732-153">A **carte** qu’emplacement de hello affiche de chaque périphérique connecté toohello solution.</span><span class="sxs-lookup"><span data-stu-id="47732-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="47732-154">solution de Hello peut utiliser les informations de tooplot hello API Bing Maps sur la carte de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="47732-155">Si votre abonnement est activé pour l’API Bing Maps Enterprise, cette fonctionnalité est automatiquement utilisée.</span><span class="sxs-lookup"><span data-stu-id="47732-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="47732-156">Dans le cas contraire, consultez hello [FAQ] [ lnk-faq] toolearn comment toomake hello dynamique de la carte.</span><span class="sxs-lookup"><span data-stu-id="47732-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="47732-157">Un panneau **Alertes** qui affiche les alertes générées lorsqu’une valeur de télémétrie ou d’OEE/KPI dépasse un seuil spécifique.</span><span class="sxs-lookup"><span data-stu-id="47732-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="47732-158">Un **l’efficacité globale équipement** Panneau de configuration qui montre les valeurs d’OEE hello d’ensemble de votre entreprise hello ou hello fabrique/production ligne/station vous visualisez.</span><span class="sxs-lookup"><span data-stu-id="47732-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="47732-159">Cette valeur est issue du niveau de l’entreprise toohello mode station hello.</span><span class="sxs-lookup"><span data-stu-id="47732-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="47732-160">la figure OEE Hello et ses éléments constitutifs peuvent être analysées davantage.</span><span class="sxs-lookup"><span data-stu-id="47732-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="47732-161">**Indicateurs de Performance clés** Panneau de configuration qui affiche le nombre hello d’unités de produits et de l’énergie utilisée par l’ensemble de votre entreprise hello ou ligne de fabrique/production hello/station vous visualisez.</span><span class="sxs-lookup"><span data-stu-id="47732-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="47732-162">Ces valeurs sont agrégées à partir d’un niveau de l’entreprise station vue toohello.</span><span class="sxs-lookup"><span data-stu-id="47732-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="47732-163">Afficher les usines</span><span class="sxs-lookup"><span data-stu-id="47732-163">View factories</span></span>

<span data-ttu-id="47732-164">Hello *fabriques* panneau affiche hello de l’emplacement géographique de toutes les fabriques de hello dans la solution de hello, leur état et la configuration actuelle de production.</span><span class="sxs-lookup"><span data-stu-id="47732-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="47732-165">À partir de la liste des emplacements hello, vous pouvez naviguer toohello autres niveaux dans la hiérarchie de la solution hello.</span><span class="sxs-lookup"><span data-stu-id="47732-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="47732-166">lignes Hello dans la liste de hello sont des liens hypertexte qui lient les détails des lignes de production hello à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="47732-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="47732-167">Il est alors possible toodrill dans les détails de la ligne de production hello et la vue du niveau toohello station.</span><span class="sxs-lookup"><span data-stu-id="47732-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="47732-168">Vous pouvez également appliquer une liste de filtres de toohello.</span><span class="sxs-lookup"><span data-stu-id="47732-168">You can also apply a filter toohello list.</span></span>

![Usines de la solution préconfigurée d’usine connectée][cf-img-factories] 

1. <span data-ttu-id="47732-170">Hello **Panneau de configuration de fabrique** affiche hello liste fabrique pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="47732-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="47732-171">liste des paramètres d’usine Hello affiche initialement les fabriques de six créés par le processus d’approvisionnement de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="47732-172">Vous pouvez ajouter la solution de toohello d’autres appareils simulé et physique.</span><span class="sxs-lookup"><span data-stu-id="47732-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="47732-173">Détails de hello tooview d’une fabrique, cliquez sur une ligne hello dans la liste des paramètres d’usine hello.</span><span class="sxs-lookup"><span data-stu-id="47732-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="47732-174">Détails de hello tooview d’une ligne de production, cliquez sur la ligne hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="47732-175">tooview hello publié nœuds OPC UA d’une station sur la ligne de production hello, cliquez sur la ligne dans la liste de hello hello.</span><span class="sxs-lookup"><span data-stu-id="47732-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="47732-176">tooview plus d’informations sur un nœud spécifique dans la console de hello, cliquez sur la ligne hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="47732-177">Cette action lance le panneau de configuration hello contexte avec des visualisations de temps série Insights.</span><span class="sxs-lookup"><span data-stu-id="47732-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="47732-178">Cliquez sur ces graphiques toodo une analyse plus approfondie dans un environnement hello temps série Insights de l’Explorateur.</span><span class="sxs-lookup"><span data-stu-id="47732-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="47732-179">Afficher la carte</span><span class="sxs-lookup"><span data-stu-id="47732-179">View map</span></span>

<span data-ttu-id="47732-180">Si votre abonnement a accès toohello API Bing Maps, hello *fabriques* carte affiche géographique hello et l’état de toutes les fabriques de hello dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="47732-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="47732-181">toodrill dans les détails d’emplacement hello, cliquez sur emplacements hello affichés sur la carte de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Carte de la solution préconfigurée d’usine connectée][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="47732-183">Afficher les alertes</span><span class="sxs-lookup"><span data-stu-id="47732-183">View alerts</span></span>

<span data-ttu-id="47732-184">Hello **alerte** Panneau de configuration vous présente les alertes générées en raison tooa signalé valeur ou une valeur calculée de OEE/indicateur de performance clé dépasse son seuil configuré.</span><span class="sxs-lookup"><span data-stu-id="47732-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="47732-185">Ce volet affiche les alertes à chaque niveau de hiérarchie hello, à partir de la vue globale de hello station vue toohello.</span><span class="sxs-lookup"><span data-stu-id="47732-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="47732-186">alertes de Hello contient une description de l’alerte de hello, date, heure, emplacement et le nombre d’occurrences.</span><span class="sxs-lookup"><span data-stu-id="47732-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="47732-187">Vous pouvez exploiter les toohello données ayant provoqué l’alerte de hello à l’aide de hello les données de série un aperçu en temps.</span><span class="sxs-lookup"><span data-stu-id="47732-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="47732-188">Hello temps série Insights données sont visualisées dans hello alertes le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="47732-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="47732-189">Si vous êtes un administrateur, vous pouvez effectuer les actions par défaut sur les alertes hello telles que :</span><span class="sxs-lookup"><span data-stu-id="47732-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="47732-190">Alerte de fermer hello.</span><span class="sxs-lookup"><span data-stu-id="47732-190">Close hello alert.</span></span>
* <span data-ttu-id="47732-191">Confirmer l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="47732-192">Vous pouvez facultativement effectuer d’autres actions plus complexes.</span><span class="sxs-lookup"><span data-stu-id="47732-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="47732-193">Par exemple, pour hello pression OPC UA nœud Hello Assembly, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="47732-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="47732-194">Affichez des informations de support dans une page web dans une nouvelle fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="47732-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="47732-195">Limiter la cause hello d’alerte de hello en appelant une méthode OPC UA sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="47732-196">Supprimez la disponibilité hello des actions par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-196">Suppress hello availability of hello default actions.</span></span>

    ![Alertes de la solution préconfigurée d’usine connectée][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="47732-198">Ces alertes sont générées par les règles spécifiées dans un fichier de configuration de solution de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="47732-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="47732-199">Ces règles peuvent générer des alertes lorsque hello OEE ou des chiffres de l’indicateur de performance clé ou des valeurs de nœud de UA OPC qui dépassent leur seuil configuré.</span><span class="sxs-lookup"><span data-stu-id="47732-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="47732-200">Hello **panneau d’alertes** affiche hello alertes générées dans cette solution.</span><span class="sxs-lookup"><span data-stu-id="47732-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="47732-201">Détails de hello tooview d’une alerte, cliquez sur l’alerte hello dans Panneau de configuration hello alertes.</span><span class="sxs-lookup"><span data-stu-id="47732-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="47732-202">toofurther analyser les données d’alerte hello, cliquez sur le graphique des hello dans l’environnement de l’Explorateur hello panneau alerte tooopen hello série un aperçu en temps.</span><span class="sxs-lookup"><span data-stu-id="47732-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="47732-203">tooaddress hello alerte, plusieurs actions sont disponibles dans le panneau de configuration alerte hello.</span><span class="sxs-lookup"><span data-stu-id="47732-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="47732-204">Choisir l’option appropriée de hello pour vous et cliquez sur hello exécuter bouton d’action de commande.</span><span class="sxs-lookup"><span data-stu-id="47732-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="47732-205">Afficher l’efficacité globale de l’équipement</span><span class="sxs-lookup"><span data-stu-id="47732-205">View overall equipment efficiency</span></span>

<span data-ttu-id="47732-206">Taux OEE hello l’efficacité des processus de fabrication hello à l’aide d’une clé paramètres opérationnels liés à la production.</span><span class="sxs-lookup"><span data-stu-id="47732-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="47732-207">OEE est une mesure standard calculée en multipliant le taux de disponibilité hello, taux de performances et le taux de qualité de l’industrie : OEE = disponibilité x qualité des performances x.</span><span class="sxs-lookup"><span data-stu-id="47732-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE de la solution préconfigurée d’usine connectée][cf-img-oee]

1. <span data-ttu-id="47732-209">tooview OEE pour n’importe quel niveau de hiérarchie de hello, accédez à vue spécifique de toohello vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="47732-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="47732-210">Hello OEE pour cette vue affiche dans le panneau hello avec chacun des éléments hello qui composent hello pourcentage OEE.</span><span class="sxs-lookup"><span data-stu-id="47732-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="47732-211">toofurther analyser hello OEE pour n’importe quel niveau de données de hiérarchie hello, cliquez sur les hello OEE, de disponibilité, de performances ou de pourcentage de la qualité.</span><span class="sxs-lookup"><span data-stu-id="47732-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="47732-212">Contexte s’affiche un aperçu en temps série alimenté de visualisations qui affiche les données hello dernière heure, des dernières 24 heures et ces 7 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="47732-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![Visualisation TSI de la solution préconfigurée d’usine connectée][cf-img-tsi-visualization]

3. <span data-ttu-id="47732-214">toofurther analyser les données d’alerte hello, cliquez sur graphique hello dans Panneau de configuration alerte hello.</span><span class="sxs-lookup"><span data-stu-id="47732-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="47732-215">Cette action ouvre l’environnement de l’Explorateur hello série un aperçu en temps.</span><span class="sxs-lookup"><span data-stu-id="47732-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![Explorateur TSI de la solution préconfigurée d’usine connectée][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="47732-217">Afficher les indicateurs de performance clés</span><span class="sxs-lookup"><span data-stu-id="47732-217">View Key Performance Indicators</span></span>

<span data-ttu-id="47732-218">solution de Hello fournit deux indicateurs de performance clés, *unités par heure* et *énergie utilisée en kWh*.</span><span class="sxs-lookup"><span data-stu-id="47732-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI de la solution préconfigurée d’usine connectée][cf-img-kpi]

1. <span data-ttu-id="47732-220">unités de tooview par heure ou de l’énergie utilisée pour n’importe quel niveau de hiérarchie de hello, accédez à vue spécifique de toohello vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="47732-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="47732-221">unités Hello par heure et de l’énergie utilisée affichage dans le panneau de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="47732-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="47732-222">unités de tooanalyze par heure ou de l’énergie utilisée pour n’importe quel niveau de hiérarchie hello en outre, cliquez sur la jauge hello Bonjour **indicateurs de Performance clés** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="47732-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="47732-223">Contexte s’affiche avec les visualisations sous tension un aperçu en temps série qui vous tooview des données à partir de hello dernière heure, hello des dernières 24 heures et ces 7 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="47732-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="47732-224">Analyse du scénario</span><span class="sxs-lookup"><span data-stu-id="47732-224">Scenario review</span></span>

<span data-ttu-id="47732-225">Dans ce scénario, vous analysé vos valeurs fabriques OEE et indicateurs de performance clés, dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="47732-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="47732-226">Vous avez puis utilisé un aperçu en temps série tooprovide plus d’informations toohelp affiner davantage les données de télémétrie hello pour toohelp OEE et indicateurs de performance clés à la détection des anomalies.</span><span class="sxs-lookup"><span data-stu-id="47732-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="47732-227">Vous avez également utilisé des problèmes de tooview panneau alerte hello avec votre fabriques et que vous avez utilisé l’alerte hello tooresolve hello actions tooyou disponibles.</span><span class="sxs-lookup"><span data-stu-id="47732-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="47732-228">Autres fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="47732-228">Other features</span></span>

<span data-ttu-id="47732-229">Hello les sections suivantes décrire certaines fonctionnalités de solution de fabrique hello connecté qui ne sont pas décrites dans le scénario précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="47732-230">Appliquer des filtres</span><span class="sxs-lookup"><span data-stu-id="47732-230">Apply filters</span></span>

1. <span data-ttu-id="47732-231">Cliquez sur hello **chevron** toodisplay une liste de filtres disponibles dans le panneau d’emplacements hello en usine ou hello alertes.</span><span class="sxs-lookup"><span data-stu-id="47732-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="47732-232">Panneau de configuration de filtres Hello s’affiche pour vous.</span><span class="sxs-lookup"><span data-stu-id="47732-232">hello filters panel is displayed for you.</span></span> 

    ![Filtres de la solution préconfigurée d’usine connectée][cf-img-alert-filter]

3. <span data-ttu-id="47732-234">Choisissez le filtre hello dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="47732-234">Choose hello filter that you require.</span></span> <span data-ttu-id="47732-235">Il est également possible tootype le texte libre dans les champs de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="47732-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="47732-236">Hello filtre est ensuite appliqué pour vous.</span><span class="sxs-lookup"><span data-stu-id="47732-236">hello filter is then applied for you.</span></span> <span data-ttu-id="47732-237">état de filtre Hello est également indiqué dans le tableau de bord hello via un graphique en entonnoir qui affiche les fabriques de hello et des alertes de tables.</span><span class="sxs-lookup"><span data-stu-id="47732-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Filtres de la solution préconfigurée d’usine connectée][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="47732-239">Un filtre actif n’affecte pas les valeurs OEE et l’indicateur de performance clé des hello affichée, elle filtre uniquement le contenu de liste hello.</span><span class="sxs-lookup"><span data-stu-id="47732-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="47732-240">tooclear un filtre, cliquez sur la forme d’entonnoir hello et cliquez sur filtre dans le panneau de contexte de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="47732-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="47732-241">Hello texte **tous les** s’affiche dans les fabriques hello et des alertes de tables.</span><span class="sxs-lookup"><span data-stu-id="47732-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="47732-242">Parcourir un serveur OPC UA</span><span class="sxs-lookup"><span data-stu-id="47732-242">Browse an OPC UA server</span></span>

<span data-ttu-id="47732-243">Lorsque vous déployez la solution de hello préconfiguré, vous déployez automatiquement des serveurs OPC UA simulés auxquelles vous pouvez accéder via l’Explorateur de solutions hello.</span><span class="sxs-lookup"><span data-stu-id="47732-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="47732-244">Ces serveurs sont des *serveurs OPC UA simulés*.</span><span class="sxs-lookup"><span data-stu-id="47732-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="47732-245">Serveurs simulés facilitent vous tooexperiment avec solution hello préconfiguré sans hello besoin toodeploy réels des serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="47732-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="47732-246">Si vous ne souhaitez pas tooconnect une solution de toohello server OPC UA réelle, consultez hello [connecter votre solution de fabrique préconfiguré OPC UA appareil toohello connecté] [ lnk-connect-cf] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="47732-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="47732-247">Cliquez sur hello **icône de fabrique** dans la barre de navigation du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="47732-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Explorateur de serveur de la solution préconfigurée d’usine connectée][cf-img-server-browser]

2. <span data-ttu-id="47732-249">Choisissez un des serveurs de hello à partir de la liste prédéfinie de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="47732-250">Cette liste affiche les serveurs hello qui sont déployées automatiquement dans les solutions hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="47732-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Sélection de serveur de la solution préconfigurée d’usine connectée][cf-img-server-choice]

3. <span data-ttu-id="47732-252">Cliquez sur **Connecter**. Une boîte de dialogue de sécurité s’affiche.</span><span class="sxs-lookup"><span data-stu-id="47732-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="47732-253">Pour la simulation de hello, il est sécurisé tooclick **continuer**</span><span class="sxs-lookup"><span data-stu-id="47732-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="47732-254">tooexpand un des nœuds hello dans l’arborescence du serveur hello, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="47732-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="47732-255">Les nœuds qui publient des données de télémétrie sont indiqués par une coche.</span><span class="sxs-lookup"><span data-stu-id="47732-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Arborescence de serveur de la solution préconfigurée d’usine connectée][cf-img-server-tree]

5. <span data-ttu-id="47732-257">Cliquez sur un élément de tooread, écrire, publier ou appeler ce nœud.</span><span class="sxs-lookup"><span data-stu-id="47732-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="47732-258">tooyou de Hello actions disponibles dépendent de vos autorisations et les attributs hello du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="47732-259">Hello lire option toodisplays un panneau de contexte montrant la valeur hello du nœud spécifique de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="47732-260">Hello écrire option affiche un panneau de contexte dans lequel vous pouvez entrer une nouvelle valeur.</span><span class="sxs-lookup"><span data-stu-id="47732-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="47732-261">option d’appel Hello affiche un nœud où vous pouvez entrer des paramètres de hello pour l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="47732-262">Publier un nœud</span><span class="sxs-lookup"><span data-stu-id="47732-262">Publish a node</span></span>

<span data-ttu-id="47732-263">Lorsque vous parcourez un *server de OPC UA simulé*, vous pouvez également choisir toopublish nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="47732-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="47732-264">Vous pouvez analyser la télémétrie hello à partir de ces nœuds dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="47732-265">Ces *simulée les serveurs OPC UA* rendre tooexperiment facile avec les solutions hello préconfiguré sans déployer les appareils physiques réelles.</span><span class="sxs-lookup"><span data-stu-id="47732-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="47732-266">Parcourir le nœud tooa Bonjour arborescence OPC UA serveur que vous souhaitez toopublish.</span><span class="sxs-lookup"><span data-stu-id="47732-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="47732-267">Cliquez sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-267">Right-click hello node.</span></span>

3. <span data-ttu-id="47732-268">Choisissez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="47732-268">Choose **Publish**.</span></span>

    ![L’usine connectée publie le nœud][cf-img-publish-node]

4. <span data-ttu-id="47732-270">Un panneau de contexte s’affiche qui indique que hello publication a réussi.</span><span class="sxs-lookup"><span data-stu-id="47732-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="47732-271">nœud de Hello apparaît dans la vue de niveau station hello avec une coche à côté de lui.</span><span class="sxs-lookup"><span data-stu-id="47732-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Réussite de la publication de la solution préconfigurée d’usine connectée][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="47732-273">Commande et contrôle</span><span class="sxs-lookup"><span data-stu-id="47732-273">Command and control</span></span>

<span data-ttu-id="47732-274">fabrique de Hello connecté vous permet de commande et contrôler vos périphériques directement à partir de cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="47732-275">Vous pouvez utiliser cette tooalerts toorespond de fonction générés par le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="47732-276">Par exemple, vous pouvez envoyer un périphérique toohello de commande à partir du cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="47732-277">Vous pouvez rechercher des commandes disponibles de hello Bonjour **StationCommands** nœud Bonjour arborescence du navigateur OPC UA serveurs.</span><span class="sxs-lookup"><span data-stu-id="47732-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="47732-278">Dans ce scénario, vous ouvrez une soupape de version sur la station d’assembly hello d’une ligne de production de Munich.</span><span class="sxs-lookup"><span data-stu-id="47732-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="47732-279">toouse hello commande fonctionnalités de contrôle, vous devez être Bonjour **administrateur** rôle pour hello préconfiguré de déploiement de solutions.</span><span class="sxs-lookup"><span data-stu-id="47732-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="47732-280">Parcourir toohello **StationCommands** nœud Bonjour arborescence du navigateur OPC UA serveur.</span><span class="sxs-lookup"><span data-stu-id="47732-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="47732-281">Choisissez la commande hello que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="47732-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="47732-282">Cliquez sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-282">Right-click hello node.</span></span>

4. <span data-ttu-id="47732-283">Choisissez **Appel**.</span><span class="sxs-lookup"><span data-stu-id="47732-283">Choose **Call**.</span></span>

    ![Commande d’appel de la solution préconfigurée d’usine connectée][cf-img-call-command]

5. <span data-ttu-id="47732-285">Un panneau de contexte s’affiche pour vous informer sur lequel la méthode que vous êtes sur toocall et les détails de paramètre s’applique.</span><span class="sxs-lookup"><span data-stu-id="47732-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="47732-286">Choisissez **Appel**.</span><span class="sxs-lookup"><span data-stu-id="47732-286">Choose **Call**.</span></span>

    ![Contexte d’appel de la solution préconfigurée d’usine connectée][cf-img-call-context]

7. <span data-ttu-id="47732-288">Panneau de configuration de contexte Hello est mise à jour tooinform que hello d’appel de méthode a réussi.</span><span class="sxs-lookup"><span data-stu-id="47732-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="47732-289">Vous pouvez vérifier l’appel hello a réussi en lisant la valeur hello du nœud de pression de hello mis à jour en raison de l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Réussite de l’appel de la solution préconfigurée d’usine connectée][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="47732-291">Coulisses de hello</span><span class="sxs-lookup"><span data-stu-id="47732-291">Behind hello scenes</span></span>

<span data-ttu-id="47732-292">Lorsque vous déployez une solution préconfigurée, processus de déploiement hello crée plusieurs ressources Bonjour abonnement Azure que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="47732-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="47732-293">Vous pouvez afficher ces ressources Bonjour Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="47732-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="47732-294">processus de déploiement Hello crée un **groupe de ressources** avec un nom basé sur le nom de hello que vous choisissez pour votre solution préconfigurée :</span><span class="sxs-lookup"><span data-stu-id="47732-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Solution préconfigurée Bonjour portail Azure][img-cf-portal]

<span data-ttu-id="47732-296">Vous pouvez afficher les paramètres de hello de chaque ressource en la sélectionnant dans la liste de hello des ressources dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="47732-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="47732-297">Vous pouvez également afficher le code source de hello pour les solutions hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="47732-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="47732-298">Hello fabrique connecté préconfiguré solution le code source est Bonjour [azure iot-connecté-usine] [ lnk-cfgithub] référentiel GitHub :</span><span class="sxs-lookup"><span data-stu-id="47732-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="47732-299">Lorsque vous avez terminé, vous pouvez supprimer la solution de hello préconfiguré à partir de votre abonnement Azure sur hello [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="47732-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="47732-300">Ce site vous permet de supprimer tooeasily que tous hello des ressources qui ont été configurés lors de la création de solutions de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="47732-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="47732-301">tooensure que vous supprimez tous les éléments liés toohello préconfiguré solution, supprimez-le sur hello [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="47732-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="47732-302">Ne supprimez pas le groupe de ressources hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="47732-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47732-303">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47732-303">Next Steps</span></span>

<span data-ttu-id="47732-304">Maintenant que vous avez déployé une solution de travail préconfiguré, vous pouvez continuer de prise en main de IoT Suite en lisant hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="47732-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="47732-305">[Procédure pas à pas de la solution préconfigurée d’usine connectée][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="47732-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="47732-306">[Connecter votre solution de fabrique connecté préconfiguré toohello périphérique][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="47732-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="47732-307">[Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="47732-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md