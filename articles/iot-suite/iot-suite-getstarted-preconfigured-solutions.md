---
title: "aaaGet main préconfiguré solutions | Documents Microsoft"
description: "Suivez ce didacticiel toolearn comment toodeploy un Azure IoT Suite solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="b4be7-103">Prise en main des solutions hello préconfiguré</span><span class="sxs-lookup"><span data-stu-id="b4be7-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="b4be7-104">Azure IoT Suite [préconfiguré solutions] [ lnk-preconfigured-solutions] combiner plusieurs Azure IoT services toodeliver bout en bout pour les solutions qui implémentent des scénarios d’entreprise IoT.</span><span class="sxs-lookup"><span data-stu-id="b4be7-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="b4be7-105">Hello *surveillance à distance* solution préconfigurée connecte tooand surveille vos appareils.</span><span class="sxs-lookup"><span data-stu-id="b4be7-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="b4be7-106">Vous pouvez utiliser des flux de hello hello solution tooanalyze de données à partir de vos appareils et les résultats de l’entreprise tooimprove en rendant les processus à répondre automatiquement toothat des flux de données.</span><span class="sxs-lookup"><span data-stu-id="b4be7-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="b4be7-107">Ce didacticiel vous montre comment la surveillance à distance de tooprovision hello préconfiguré solution.</span><span class="sxs-lookup"><span data-stu-id="b4be7-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="b4be7-108">Il vous guide également dans les fonctionnalités de base hello de solution de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="b4be7-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="b4be7-109">Vous pouvez accéder à la plupart de ces fonctionnalités à partir de la solution de hello *tableau de bord* qui déploie dans le cadre de la solution de hello préconfiguré :</span><span class="sxs-lookup"><span data-stu-id="b4be7-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Tableau de bord de solution préconfigurée de surveillance à distance][img-dashboard]

<span data-ttu-id="b4be7-111">toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="b4be7-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b4be7-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="b4be7-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b4be7-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="b4be7-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="b4be7-114">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="b4be7-114">Scenario overview</span></span>

<span data-ttu-id="b4be7-115">Lorsque vous déployez hello solution préconfigurée de surveillance à distance, il est préremplie avec les ressources qui permettent de vous toostep via un scénario courant de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="b4be7-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="b4be7-116">Dans ce scénario, solution de toohello connecté plusieurs périphériques sont reporting des valeurs de température inattendue.</span><span class="sxs-lookup"><span data-stu-id="b4be7-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="b4be7-117">Hello sections suivantes vous indiquent comment procéder pour :</span><span class="sxs-lookup"><span data-stu-id="b4be7-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="b4be7-118">Identifier les périphériques hello envoyez des valeurs de température inattendu.</span><span class="sxs-lookup"><span data-stu-id="b4be7-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="b4be7-119">Configurez ces périphériques toosend plus détaillées que les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="b4be7-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="b4be7-120">Résoudre les problème de hello en mettant à jour de microprogramme hello sur ces appareils.</span><span class="sxs-lookup"><span data-stu-id="b4be7-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="b4be7-121">Vérifiez que votre action a résolu le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="b4be7-122">Une fonctionnalité clé de ce scénario est que vous pouvez effectuer toutes ces actions à distance à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="b4be7-123">Vous n’avez pas besoin d’appareils de toohello d’accès physique.</span><span class="sxs-lookup"><span data-stu-id="b4be7-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="b4be7-124">Tableau de bord View hello solution</span><span class="sxs-lookup"><span data-stu-id="b4be7-124">View hello solution dashboard</span></span>

<span data-ttu-id="b4be7-125">tableau de bord Hello solution vous permet de solution de hello déployé toomanage.</span><span class="sxs-lookup"><span data-stu-id="b4be7-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="b4be7-126">Par exemple, vous pouvez afficher les données de télémétrie, ajouter des appareils et configurer des règles.</span><span class="sxs-lookup"><span data-stu-id="b4be7-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="b4be7-127">Lorsque l’approvisionnement hello est terminé et vignette hello pour votre solution préconfigurée indique **prêt**, choisissez **lancer** tooopen votre portail de solution de surveillance à distance dans un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="b4be7-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Lancer la solution de hello préconfiguré][img-launch-solution]

1. <span data-ttu-id="b4be7-129">Par défaut, portail de solution hello affiche hello *tableau de bord*.</span><span class="sxs-lookup"><span data-stu-id="b4be7-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="b4be7-130">Vous pouvez naviguer tooother des zones du portail de solution hello à l’aide du menu de hello sur la partie gauche de la page de hello hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Tableau de bord de solution préconfigurée de surveillance à distance][img-menu]

<span data-ttu-id="b4be7-132">tableau de bord Hello affiche hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b4be7-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="b4be7-133">Une carte qui affiche l’emplacement hello de chaque périphérique connecté toohello solution.</span><span class="sxs-lookup"><span data-stu-id="b4be7-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="b4be7-134">Lorsque vous exécutez la solution de hello pour la première fois, il existe des 25 périphériques simulés.</span><span class="sxs-lookup"><span data-stu-id="b4be7-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="b4be7-135">périphériques simulés Hello sont implémentés en tant que tâches Web Azure et les solutions hello utilise hello API Bing Maps tooplot d’informations sur la carte de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="b4be7-136">Consultez hello [FAQ] [ lnk-faq] toolearn comment toomake hello dynamique de la carte.</span><span class="sxs-lookup"><span data-stu-id="b4be7-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="b4be7-137">Un panneau **Historique de télémétrie** qui trace la télémétrie de l’humidité et de la température d’un appareil sélectionné en temps quasi-réel et affiche les données d’agrégation telles que l’humidité maximale, minimale et moyenne.</span><span class="sxs-lookup"><span data-stu-id="b4be7-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="b4be7-138">Un panneau **Historique des alertes** qui affiche les alarmes récentes lorsqu’une valeur de télémétrie a dépassé un seuil défini.</span><span class="sxs-lookup"><span data-stu-id="b4be7-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="b4be7-139">Vous pouvez définir vos propres alarmes dans les exemples de toohello plus créés par la solution de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="b4be7-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="b4be7-140">Un panneau **Tâches** qui affiche des informations sur les travaux planifiés.</span><span class="sxs-lookup"><span data-stu-id="b4be7-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="b4be7-141">Vous pouvez planifier vos propres tâches sur la page **Gestion des tâches**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="b4be7-142">Afficher les alarmes</span><span class="sxs-lookup"><span data-stu-id="b4be7-142">View alarms</span></span>

<span data-ttu-id="b4be7-143">panneau d’historique Hello alarme montre que cinq appareils sont reporting supérieure à celle des valeurs de télémétrie attendu.</span><span class="sxs-lookup"><span data-stu-id="b4be7-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Historique TODO alarme sur le tableau de bord de solution hello][img-alarms]

> [!NOTE]
> <span data-ttu-id="b4be7-145">Ces alertes sont générées par une règle qui est incluse dans la solution de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="b4be7-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="b4be7-146">Cette règle génère une alerte lorsque la valeur de la température hello envoyé par un périphérique dépasse 60.</span><span class="sxs-lookup"><span data-stu-id="b4be7-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="b4be7-147">Vous pouvez définir vos propres règles et les actions en choisissant [règles](#add-a-rule) et [Actions](#add-an-action) dans le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="b4be7-148">Afficher les appareils</span><span class="sxs-lookup"><span data-stu-id="b4be7-148">View devices</span></span>

<span data-ttu-id="b4be7-149">Hello *périphériques* liste affiche tous les périphériques de hello inscrit dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="b4be7-150">À partir de la liste des appareils hello vous pouvez afficher et modifier les métadonnées de l’appareil, ajouter ou supprimer des appareils et appeler des méthodes sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="b4be7-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="b4be7-151">Vous pouvez filtrer et trier la liste hello des périphériques dans la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="b4be7-152">Vous pouvez également personnaliser les colonnes hello indiquées dans la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="b4be7-153">Choisissez **périphériques** liste des appareils tooshow hello pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="b4be7-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Liste des appareils hello vue dans le portail de solution hello][img-devicelist]

1. <span data-ttu-id="b4be7-155">liste des appareils Hello affiche initialement 25 périphériques simulés créés par le processus d’approvisionnement de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="b4be7-156">Vous pouvez ajouter la solution de toohello d’autres appareils simulé et physique.</span><span class="sxs-lookup"><span data-stu-id="b4be7-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="b4be7-157">Détails de hello tooview d’un appareil, choisissez un périphérique dans la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Afficher les détails de l’appareil hello dans le portail de solution hello][img-devicedetails]

<span data-ttu-id="b4be7-159">Hello **détails de l’appareil** panneau contient six sections :</span><span class="sxs-lookup"><span data-stu-id="b4be7-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="b4be7-160">Une collection de liens qui activent vous toocustomize hello icône périphérique, désactivez hello périphérique, ajouter une règle, appellent une méthode ou envoyant une commande.</span><span class="sxs-lookup"><span data-stu-id="b4be7-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="b4be7-161">Pour voir une comparaison des commandes (messages appareil-à-cloud) et des méthodes (méthodes directes), consultez [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="b4be7-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="b4be7-162">Hello **appareil double - balises** section vous permet de valeurs de balise tooedit pour appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="b4be7-163">Vous pouvez afficher des valeurs de balise dans la liste des appareils hello et utilisez liste des appareils balise valeurs toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="b4be7-164">Hello **appareil double - propriétés de souhaité** section vous permet de tooset propriété valeurs toobe envoyé toohello appareil.</span><span class="sxs-lookup"><span data-stu-id="b4be7-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="b4be7-165">Hello **appareil double - a signalé des propriétés** section affiche les valeurs de propriété envoyés à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="b4be7-166">Hello **propriétés de l’appareil** section affiche les informations de Registre des identités hello tels que le périphérique de hello clés id et l’authentification.</span><span class="sxs-lookup"><span data-stu-id="b4be7-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="b4be7-167">Hello **travaux récents** section affiche des informations sur tous les travaux qui ont ciblés récemment cet appareil.</span><span class="sxs-lookup"><span data-stu-id="b4be7-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="b4be7-168">Filtrer la liste des appareils hello</span><span class="sxs-lookup"><span data-stu-id="b4be7-168">Filter hello device list</span></span>

<span data-ttu-id="b4be7-169">Vous pouvez utiliser un filtre toodisplay que les périphériques qui envoient des valeurs de température inattendue.</span><span class="sxs-lookup"><span data-stu-id="b4be7-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="b4be7-170">Hello solution préconfigurée de surveillance à distance inclut hello **appareils défectueux** filtrer les appareils tooshow avec une valeur de température moyenne supérieure à 60.</span><span class="sxs-lookup"><span data-stu-id="b4be7-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="b4be7-171">Vous pouvez également [créer vos propres filtres](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="b4be7-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="b4be7-172">Choisissez **ouvrir l’enregistrement de filtre** toodisplay une liste de filtres disponibles.</span><span class="sxs-lookup"><span data-stu-id="b4be7-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="b4be7-173">Puis choisissez **appareils défectueux** filtre de hello tooapply :</span><span class="sxs-lookup"><span data-stu-id="b4be7-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Afficher la liste hello des filtres][img-unhealthy-filter]

1. <span data-ttu-id="b4be7-175">liste des appareils Hello affiche maintenant uniquement les périphériques avec une valeur de température moyenne supérieure à 60.</span><span class="sxs-lookup"><span data-stu-id="b4be7-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Vue hello périphérique filtrés liste appareils défectueux][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="b4be7-177">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="b4be7-177">Update desired properties</span></span>

<span data-ttu-id="b4be7-178">Vous avez désormais identifié un ensemble d’appareils nécessitant une correction.</span><span class="sxs-lookup"><span data-stu-id="b4be7-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="b4be7-179">Toutefois, vous décidez que la fréquence de données hello de 15 secondes n’est pas suffisant pour un diagnostic clair du problème de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="b4be7-180">La modification hello télémétrie fréquence toofive secondes tooprovide vous avec toobetter de points de données plus diagnostiquer les problème de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="b4be7-181">Vous pouvez transmettre cette configuration modification tooyour à distance les appareils à partir du portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="b4be7-182">Vous pouvez modifier hello qu’une seule fois, évaluer l’impact de hello et ensuite agir sur les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="b4be7-183">Suivez ces étapes de toorun une opération de changement de hello **TelemetryInterval** souhaité de propriété pour les appareils hello affectée.</span><span class="sxs-lookup"><span data-stu-id="b4be7-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="b4be7-184">Lorsque les appareils hello réception hello nouvelle **TelemetryInterval** valeur de propriété, ils changent leurs données de télémétrie toosend configuration toutes les cinq secondes au lieu de toutes les 15 secondes :</span><span class="sxs-lookup"><span data-stu-id="b4be7-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="b4be7-185">Lors de l’affichage liste hello de périphériques défectueux dans la liste des appareils hello, choisissez **planificateur**, puis **double de périphérique modifier**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="b4be7-186">Appelez la tâche de hello **intervalle de modification de données de télémétrie**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="b4be7-187">Modifier la valeur hello hello **propriété souhaitée** nom **souhaitée. Config.TelemetryInterval** toofive secondes.</span><span class="sxs-lookup"><span data-stu-id="b4be7-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="b4be7-188">Choisissez **Planification**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-188">Choose **Schedule**.</span></span>

    ![Modifier hello TelemetryInterval propriété toofive secondes][img-change-interval]

1. <span data-ttu-id="b4be7-190">Vous pouvez surveiller la progression hello du travail hello hello **des tâches de gestion** page hello portail.</span><span class="sxs-lookup"><span data-stu-id="b4be7-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b4be7-191">Si vous souhaitez toochange une valeur de propriété souhaitée pour un périphérique, utilisez hello **propriétés souhaitées** section Bonjour **détails de l’appareil** Panneau de configuration au lieu d’exécuter un travail.</span><span class="sxs-lookup"><span data-stu-id="b4be7-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="b4be7-192">Cette tâche définit la valeur hello hello **TelemetryInterval** souhaité de propriété en double d’appareil hello pour tous les hello périphériques sélectionnés par le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="b4be7-193">les appareils de Hello récupèrent cette valeur à partir du double du périphérique hello et mettre à jour leur comportement.</span><span class="sxs-lookup"><span data-stu-id="b4be7-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="b4be7-194">Quand un appareil récupère et traite une propriété spécifique à partir d’un double de l’appareil, il définit la propriété de valeur signalée hello correspondante.</span><span class="sxs-lookup"><span data-stu-id="b4be7-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="b4be7-195">Appeler des méthodes</span><span class="sxs-lookup"><span data-stu-id="b4be7-195">Invoke methods</span></span>

<span data-ttu-id="b4be7-196">Pendant l’exécution de tâche de hello, vous remarquez dans liste hello de périphériques défectueux que tous ces périphériques disposant d’un microprogramme ancien (inférieur à la version 1.6) versions.</span><span class="sxs-lookup"><span data-stu-id="b4be7-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Version du microprogramme pour les appareils défectueux hello a signalé l’hello de vue][img-old-firmware]

<span data-ttu-id="b4be7-198">Cette version du microprogramme peut être la cause première hello de hello inattendue, car vous savez que les autres périphériques intègres ont été récemment mis à jour tooversion 2.0 des valeurs de température.</span><span class="sxs-lookup"><span data-stu-id="b4be7-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="b4be7-199">Vous pouvez utiliser hello intégrée **anciens périphériques microprogramme** filtrer tooidentify tous les périphériques avec d’anciennes versions du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="b4be7-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="b4be7-200">À partir du portail de hello, vous pouvez ensuite à distance mettre à jour tous les appareils hello exécute toujours les anciennes versions de microprogramme :</span><span class="sxs-lookup"><span data-stu-id="b4be7-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="b4be7-201">Choisissez **ouvrir l’enregistrement de filtre** toodisplay une liste de filtres disponibles.</span><span class="sxs-lookup"><span data-stu-id="b4be7-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="b4be7-202">Puis choisissez **anciens périphériques microprogramme** filtre de hello tooapply :</span><span class="sxs-lookup"><span data-stu-id="b4be7-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Afficher la liste hello des filtres][img-old-filter]

1. <span data-ttu-id="b4be7-204">liste des appareils Hello affiche maintenant uniquement les appareils avec d’anciennes versions du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="b4be7-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="b4be7-205">Cette liste inclut hello cinq appareils identifiés par hello **appareils défectueux** filtre et trois unités supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="b4be7-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Liste de périphérique filtrés hello vue affichant les anciens périphériques][img-filtered-old-list]

1. <span data-ttu-id="b4be7-207">Choisissez **Planificateur de travaux**, puis **Appeler une méthode**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="b4be7-208">Définissez **nom de la tâche** trop**tooversion de mise à jour de microprogramme 2.0**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="b4be7-209">Choisissez **InitiateFirmwareUpdate** comme hello **méthode**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="b4be7-210">Ensemble hello **FwPackageUri** paramètre trop**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="b4be7-211">Choisissez **Planification**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-211">Choose **Schedule**.</span></span> <span data-ttu-id="b4be7-212">valeur par défaut Hello est désormais pour toorun de travail hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-212">hello default is for hello job toorun now.</span></span>

    ![Créer le microprogramme de hello tooupdate de travail des appareils de hello sélectionné][img-method-update]

> [!NOTE]
> <span data-ttu-id="b4be7-214">Si vous souhaitez tooinvoke une méthode sur un périphérique, choisissez **méthodes** Bonjour **détails de l’appareil** Panneau de configuration au lieu d’exécuter un travail.</span><span class="sxs-lookup"><span data-stu-id="b4be7-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="b4be7-215">Ce travail appelle hello **InitiateFirmwareUpdate** méthode directe sur tous les appareils hello sélectionnés par le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="b4be7-216">Appareils répondent immédiatement tooIoT Hub et puis initier de façon asynchrone les processus de mise à jour de microprogramme hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="b4be7-217">les appareils Hello fournissent les informations d’état sur le processus de mise à jour de microprogramme hello via des valeurs de propriété signalé, comme indiqué dans hello suivant des captures d’écran.</span><span class="sxs-lookup"><span data-stu-id="b4be7-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="b4be7-218">Choisissez hello **Actualiser** icône tooupdate hello plus d’informations dans les listes de périphérique et la tâche hello :</span><span class="sxs-lookup"><span data-stu-id="b4be7-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="b4be7-219">![Liste de tâches montrant l’exécution de liste de mise à jour de microprogramme hello][img-update-1]
![liste des appareils montrant l’état de mise à jour de microprogramme][img-update-2]
![travail liste affichant hello microprogramme mise à jour la liste complète][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="b4be7-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="b4be7-220">Dans un environnement de production, vous pouvez planifier des travaux toorun pendant une fenêtre de maintenance désigné.</span><span class="sxs-lookup"><span data-stu-id="b4be7-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="b4be7-221">Analyse du scénario</span><span class="sxs-lookup"><span data-stu-id="b4be7-221">Scenario review</span></span>

<span data-ttu-id="b4be7-222">Dans ce scénario, vous identifié un problème potentiel avec certains de vos périphériques à distance à l’aide de l’historique de hello alarme sur le tableau de bord hello et un filtre.</span><span class="sxs-lookup"><span data-stu-id="b4be7-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="b4be7-223">Vous les filtres utilisés hello et un tooremotely de travail configurent hello appareils tooprovide plus d’informations toohelp diagnostiquer le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="b4be7-224">Enfin, vous avez utilisé un filtre et une maintenance tooschedule du travail sur les appareils hello affectée.</span><span class="sxs-lookup"><span data-stu-id="b4be7-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="b4be7-225">Si vous retournez toohello le tableau de bord, vous pouvez vérifier qu’il n’y a n’est plus n’importe quel alarmes provenant d’appareils dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="b4be7-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="b4be7-226">Vous pouvez utiliser un filtre tooverify qui hello microprogramme est à jour sur tous les appareils hello dans votre solution et qu’il existe des appareils défectueux n’y a plus :</span><span class="sxs-lookup"><span data-stu-id="b4be7-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtre indiquant que tous les appareils disposent d’un microprogramme à jour][img-updated]

![Filtre indiquant que tous les appareils sont sains][img-healthy]

## <a name="other-features"></a><span data-ttu-id="b4be7-229">Autres fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="b4be7-229">Other features</span></span>

<span data-ttu-id="b4be7-230">Hello sections suivantes décrivent certaines fonctionnalités de hello solution préconfigurée de surveillance à distance qui ne sont pas décrits dans le cadre du scénario précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="b4be7-231">Personnaliser les colonnes</span><span class="sxs-lookup"><span data-stu-id="b4be7-231">Customize columns</span></span>

<span data-ttu-id="b4be7-232">Vous pouvez personnaliser les informations de hello affichées dans la liste des appareils hello en choisissant **éditeur colonne**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="b4be7-233">Vous pouvez ajouter et supprimer des colonnes dans lesquelles figurent des valeurs de balises et de propriétés signalées.</span><span class="sxs-lookup"><span data-stu-id="b4be7-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="b4be7-234">Vous pouvez également réorganiser et renommer les colonnes :</span><span class="sxs-lookup"><span data-stu-id="b4be7-234">You can also reorder and rename columns:</span></span>

   ![Liste des appareils colonne éditeur ion hello][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="b4be7-236">Personnaliser l’icône du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="b4be7-236">Customize hello device icon</span></span>

<span data-ttu-id="b4be7-237">Vous pouvez personnaliser hello appareil icône est affichée dans la liste des périphériques à partir de hello hello **détails de l’appareil** panneau comme suit :</span><span class="sxs-lookup"><span data-stu-id="b4be7-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="b4be7-238">Choisissez Bonjour crayon icône tooopen Bonjour **modifier l’image** Panneau de configuration pour un périphérique :</span><span class="sxs-lookup"><span data-stu-id="b4be7-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![Ouvrir l’éditeur d’image d’appareil][img-startimageedit]

1. <span data-ttu-id="b4be7-240">Soit charger une nouvelle image ou utilisez une des images existantes de hello, puis choisissez **enregistrer**:</span><span class="sxs-lookup"><span data-stu-id="b4be7-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![Modifier l’éditeur d’image d’appareil][img-imageedit]

1. <span data-ttu-id="b4be7-242">Hello image que vous venez de sélectionner affiche Bonjour **icône** colonne pour appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="b4be7-243">image de Hello est stockée dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="b4be7-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="b4be7-244">Une balise en double d’appareil hello contient une image de toohello de lien dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="b4be7-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="b4be7-245">Ajout d’un appareil</span><span class="sxs-lookup"><span data-stu-id="b4be7-245">Add a device</span></span>

<span data-ttu-id="b4be7-246">Lorsque vous déployez la solution de hello préconfiguré, vous déployez automatiquement des 25 périphériques d’exemple que vous pouvez voir dans la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="b4be7-247">Ces appareils sont des *simulations d’appareils* en cours d’exécution dans un Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="b4be7-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="b4be7-248">Appareils simulés facilitent vous tooexperiment avec solution hello préconfiguré sans hello besoin toodeploy réel physique les appareils.</span><span class="sxs-lookup"><span data-stu-id="b4be7-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="b4be7-249">Si vous ne souhaitez pas tooconnect une solution de toohello périphérique réel, consultez hello [connecter votre solution préconfigurée de surveillance à distance de toohello périphérique] [ lnk-connect-rm] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b4be7-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="b4be7-250">Hello étapes suivantes vous montrent comment tooadd une solution de toohello appareil simulé :</span><span class="sxs-lookup"><span data-stu-id="b4be7-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="b4be7-251">Parcourir la liste de périphériques de toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="b4be7-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="b4be7-252">tooadd un appareil, choisissez **+ ajouter un périphérique** dans hello bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="b4be7-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Ajouter une solution toohello préconfiguré de périphérique][img-adddevice]

1. <span data-ttu-id="b4be7-254">Choisissez **nouveau** sur hello **simulée de périphérique** vignette.</span><span class="sxs-lookup"><span data-stu-id="b4be7-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Définir les détails du nouvel appareil dans le tableau de bord][img-addnew]

   <span data-ttu-id="b4be7-256">Dans Ajout toocreating un nouvel appareil simulé, vous pouvez également ajouter un périphérique physique si vous choisissez toocreate un **personnalisé périphérique**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="b4be7-257">toolearn en savoir plus sur la connexion de périphériques physiques toohello solution, consultez [connecter votre toohello appareil IoT Suite solution préconfigurée de surveillance à distance][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="b4be7-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="b4be7-258">Sélectionnez **Me laisser définir mon propre ID d’appareil** et ajoutez un nom unique d’ID d’appareil, par exemple **monappareil_01**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="b4be7-259">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-259">Choose **Create**.</span></span>

   ![Enregistrer un nouvel appareil][img-definedevice]

1. <span data-ttu-id="b4be7-261">Dans l’étape 3 de **ajouter un appareil simulé**, choisissez **fait** liste des appareils tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="b4be7-262">Vous pouvez afficher votre appareil **en cours d’exécution** dans la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-262">You can view your device **Running** in hello device list.</span></span>

    ![Afficher le nouvel appareil dans la liste des appareils][img-runningnew]

1. <span data-ttu-id="b4be7-264">Vous pouvez également afficher hello simulée de télémétrie à partir de votre nouveau périphérique sur le tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="b4be7-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Afficher la télémétrie du nouvel appareil][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="b4be7-266">Désactiver et supprimer un appareil</span><span class="sxs-lookup"><span data-stu-id="b4be7-266">Disable and delete a device</span></span>

<span data-ttu-id="b4be7-267">Vous pouvez désactiver un appareil puis le supprimer :</span><span class="sxs-lookup"><span data-stu-id="b4be7-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Désactiver et supprimer un appareil][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="b4be7-269">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="b4be7-269">Add a rule</span></span>

<span data-ttu-id="b4be7-270">Il n’existe aucune règle pour le nouveau périphérique de hello que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="b4be7-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="b4be7-271">Dans cette section, vous ajoutez une règle qui déclenche une alerte lors de la température de hello signalés par hello nouveau périphérique dépasse 47 degrés.</span><span class="sxs-lookup"><span data-stu-id="b4be7-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="b4be7-272">Avant de commencer, notez que l’historique des données de télémétrie hello pour le nouveau périphérique de hello sur le tableau de bord hello montre la température du périphérique hello ne dépasse jamais 45 degrés.</span><span class="sxs-lookup"><span data-stu-id="b4be7-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="b4be7-273">Parcourir la liste de périphériques de toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="b4be7-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="b4be7-274">tooadd une règle pour appareil de hello, sélectionnez votre nouveau périphérique Bonjour **liste de périphériques**, puis choisissez **ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="b4be7-275">Créer une règle qui utilise **température** en tant que champ de données hello et utilise **AlarmTemp** comme hello lorsque la température de hello dépasse 47 degrés de sortie :</span><span class="sxs-lookup"><span data-stu-id="b4be7-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule]

1. <span data-ttu-id="b4be7-277">Choisissez de vos modifications, toosave **enregistrer et afficher les règles**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="b4be7-278">Choisissez **commandes** dans le volet d’informations de périphérique hello pour le nouveau périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule2]

1. <span data-ttu-id="b4be7-280">Sélectionnez **ChangeSetPointTemp** à partir de la liste de commandes hello et ensemble **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="b4be7-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="b4be7-281">Puis choisissez **Envoyer la commande** :</span><span class="sxs-lookup"><span data-stu-id="b4be7-281">Then choose **Send Command**:</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule3]

1. <span data-ttu-id="b4be7-283">Accédez toohello différé du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="b4be7-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="b4be7-284">Après un bref laps de temps, vous verrez une nouvelle entrée Bonjour **alarme historique** volet lors de la température de hello signalé par votre nouveau périphérique dépasse le seuil de degrés 47 hello :</span><span class="sxs-lookup"><span data-stu-id="b4be7-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule4]

1. <span data-ttu-id="b4be7-286">Vous pouvez consulter et modifier toutes les règles sur hello **règles** page du tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="b4be7-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Répertorier les règles d’appareil][img-rules]

1. <span data-ttu-id="b4be7-288">Vous pouvez consulter et modifier toutes les actions hello qui peuvent être effectuées dans la règle de tooa de réponse sur hello **Actions** page du tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="b4be7-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Répertorier les actions d’appareil][img-actions]

> [!NOTE]
> <span data-ttu-id="b4be7-290">Il est possible toodefine les actions qui peuvent envoyer un message électronique ou SMS dans la réponse tooa règle ou l’intégrer avec un système métier-via un [application logique][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="b4be7-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="b4be7-291">Pour plus d’informations, consultez hello [tooyour connecter une application de logique Azure IoT Suite de l’analyse à distance de solution préconfigurée][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="b4be7-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="b4be7-292">Gérer les filtres</span><span class="sxs-lookup"><span data-stu-id="b4be7-292">Manage filters</span></span>

<span data-ttu-id="b4be7-293">Dans la liste des appareils hello, vous pouvez créer, enregistrer et recharger les filtres toodisplay une liste personnalisée de concentrateur tooyour connecté de périphériques.</span><span class="sxs-lookup"><span data-stu-id="b4be7-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="b4be7-294">toocreate un filtre :</span><span class="sxs-lookup"><span data-stu-id="b4be7-294">toocreate a filter:</span></span>

1. <span data-ttu-id="b4be7-295">Choisissez l’icône de filtre hello modifier au-dessus de la liste des appareils hello :</span><span class="sxs-lookup"><span data-stu-id="b4be7-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Éditeur de filtre hello ouvert][img-editfiltericon]

1. <span data-ttu-id="b4be7-297">Bonjour **l’éditeur de filtre**, ajouter des champs de hello, d’opérateurs et de liste de valeurs toofilter hello appareil.</span><span class="sxs-lookup"><span data-stu-id="b4be7-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="b4be7-298">Vous pouvez ajouter plusieurs clauses toorefine votre filtre.</span><span class="sxs-lookup"><span data-stu-id="b4be7-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="b4be7-299">Choisissez **filtre** filtre de hello tooapply :</span><span class="sxs-lookup"><span data-stu-id="b4be7-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Créer un filtre][img-filtereditor]

1. <span data-ttu-id="b4be7-301">Dans cet exemple, la liste de hello est filtré par le fabricant et le numéro de modèle :</span><span class="sxs-lookup"><span data-stu-id="b4be7-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Liste de filtrage][img-filterelist]

1. <span data-ttu-id="b4be7-303">toosave votre filtre avec un nom personnalisé, choisissez hello **enregistrer en tant que** icône :</span><span class="sxs-lookup"><span data-stu-id="b4be7-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Enregistrer un filtre][img-savefilter]

1. <span data-ttu-id="b4be7-305">tooreapply un filtre que vous avez enregistré précédemment, choisissez hello **ouvrir l’enregistrement de filtre** icône :</span><span class="sxs-lookup"><span data-stu-id="b4be7-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Ouvrir un filtre][img-openfilter]

<span data-ttu-id="b4be7-307">Vous pouvez créer des filtres en fonction de l’id de l’appareil, de son état, des propriétés souhaitées, des propriétés signalées et des balises.</span><span class="sxs-lookup"><span data-stu-id="b4be7-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="b4be7-308">Vous ajoutez votre propre appareil tooa de balises personnalisées Bonjour **balises** section Hello **détails de l’appareil** panneau ou exécuter un travail tooupdate des balises sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="b4be7-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="b4be7-309">Bonjour **l’éditeur de filtre**, vous pouvez utiliser hello **vue avancée** tooedit hello texte de la requête directement.</span><span class="sxs-lookup"><span data-stu-id="b4be7-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="b4be7-310">Commandes</span><span class="sxs-lookup"><span data-stu-id="b4be7-310">Commands</span></span>

<span data-ttu-id="b4be7-311">À partir de hello **détails de l’appareil** Panneau de configuration, vous pouvez envoyer un périphérique toohello de commandes.</span><span class="sxs-lookup"><span data-stu-id="b4be7-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="b4be7-312">Premier démarrage d’un périphérique, il envoie plus d’informations sur hello commandes que toohello solution prend en charge.</span><span class="sxs-lookup"><span data-stu-id="b4be7-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="b4be7-313">Pour en savoir plus sur les différences de hello entre les commandes et les méthodes, consultez [options de cloud-à-appareil Azure IoT Hub][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="b4be7-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="b4be7-314">Choisissez **commandes** Bonjour **détails de l’appareil** Panneau de configuration pour le périphérique sélectionné de hello :</span><span class="sxs-lookup"><span data-stu-id="b4be7-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Commandes de l’appareil dans le tableau de bord][img-devicecommands]

1. <span data-ttu-id="b4be7-316">Sélectionnez **PingDevice** à partir de la liste de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="b4be7-317">Choisissez **Envoyer la commande**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="b4be7-318">Vous pouvez voir l’état hello de commande hello dans l’historique de commande hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-318">You can see hello status of hello command in hello command history.</span></span>

   ![État de la commande dans le tableau de bord][img-pingcommand]

<span data-ttu-id="b4be7-320">solution de Hello effectue le suivi d’état hello de chaque commande, qu'il envoie.</span><span class="sxs-lookup"><span data-stu-id="b4be7-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="b4be7-321">Initialement le résultat de hello est **en attente**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="b4be7-322">Lors de l’appareil de hello signale qu’il a exécuté la commande hello, le résultat de hello est défini trop**réussite**.</span><span class="sxs-lookup"><span data-stu-id="b4be7-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="b4be7-323">Coulisses de hello</span><span class="sxs-lookup"><span data-stu-id="b4be7-323">Behind hello scenes</span></span>

<span data-ttu-id="b4be7-324">Lorsque vous déployez une solution préconfigurée, processus de déploiement hello crée plusieurs ressources Bonjour abonnement Azure que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="b4be7-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="b4be7-325">Vous pouvez afficher ces ressources Bonjour Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="b4be7-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="b4be7-326">processus de déploiement Hello crée un **groupe de ressources** avec un nom basé sur le nom de hello que vous choisissez pour votre solution préconfigurée :</span><span class="sxs-lookup"><span data-stu-id="b4be7-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Solution préconfigurée Bonjour portail Azure][img-portal]

<span data-ttu-id="b4be7-328">Vous pouvez afficher les paramètres de hello de chaque ressource en la sélectionnant dans la liste de hello des ressources dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="b4be7-329">Vous pouvez également afficher le code source de hello pour les solutions hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="b4be7-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="b4be7-330">Bonjour à distance le contrôle de code source de solution préconfigurée est Bonjour [azure-iot-de surveillance à distance] [ lnk-rmgithub] référentiel GitHub :</span><span class="sxs-lookup"><span data-stu-id="b4be7-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="b4be7-331">Hello **DeviceAdministration** dossier contient le code source hello pour le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="b4be7-332">Hello **simulateur** dossier contient le code source hello pour les appareil simulé hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="b4be7-333">Hello **EventProcessor** dossier contient le code source hello pour hello au processus principal qui gère les données de télémétrie entrants hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="b4be7-334">Lorsque vous avez terminé, vous pouvez supprimer la solution de hello préconfiguré à partir de votre abonnement Azure sur hello [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="b4be7-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="b4be7-335">Ce site vous permet de supprimer tooeasily que tous hello des ressources qui ont été configurés lors de la création de solutions de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="b4be7-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="b4be7-336">tooensure que vous supprimez tous les éléments liés toohello préconfiguré solution, supprimez-le sur hello [azureiotsuite.com] [ lnk-azureiotsuite] de site et ne supprimez pas le groupe de ressources hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b4be7-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4be7-337">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b4be7-337">Next Steps</span></span>

<span data-ttu-id="b4be7-338">Maintenant que vous avez déployé une solution de travail préconfiguré, vous pouvez continuer de prise en main de IoT Suite en lisant hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="b4be7-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="b4be7-339">[Présentation de la solution préconfigurée de surveillance à distance][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="b4be7-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="b4be7-340">[Se connecter à votre solution préconfigurée de surveillance à distance de toohello périphérique][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="b4be7-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="b4be7-341">[Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="b4be7-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md