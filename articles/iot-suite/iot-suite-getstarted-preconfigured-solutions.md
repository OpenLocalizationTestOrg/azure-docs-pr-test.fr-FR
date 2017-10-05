---
title: "Prise en main des solutions préconfigurées | Microsoft Docs"
description: "Suivez ce didacticiel pour apprendre à déployer une solution préconfigurée Azure IoT Suite."
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
ms.openlocfilehash: 466825ab78a5ac9773d8beff69cca90ff9db6c01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="c3690-103">Prise en main des solutions préconfigurées</span><span class="sxs-lookup"><span data-stu-id="c3690-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="c3690-104">Les [solutions préconfigurées][lnk-preconfigured-solutions] d’Azure IoT Suite regroupent plusieurs services Azure IoT pour offrir des solutions de bout en bout permettant d’implémenter des scénarios IoT d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c3690-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="c3690-105">La solution préconfigurée de *surveillance à distance* se connecte et surveille vos appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="c3690-106">Cela vous permet d’analyser le flux de données de vos appareils et d’améliorer les résultats de l’entreprise grâce à des processus qui répondent automatiquement à ce flux de données.</span><span class="sxs-lookup"><span data-stu-id="c3690-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="c3690-107">Ce didacticiel montre comment configurer la solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="c3690-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="c3690-108">Il présente également les fonctionnalités de base de la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="c3690-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="c3690-109">Vous pouvez accéder à la plupart de ces fonctionnalités à partir du *tableau de bord* de solution déployé avec la solution préconfigurée :</span><span class="sxs-lookup"><span data-stu-id="c3690-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Tableau de bord de solution préconfigurée de surveillance à distance][img-dashboard]

<span data-ttu-id="c3690-111">Pour suivre ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c3690-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="c3690-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c3690-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c3690-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="c3690-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="c3690-114">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="c3690-114">Scenario overview</span></span>

<span data-ttu-id="c3690-115">Lorsque vous déployez la solution préconfigurée de surveillance à distance, elle est préremplie avec les ressources qui vous permettent de parcourir un scénario courant de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="c3690-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="c3690-116">Dans ce scénario, plusieurs appareils connectés à la solution présentent des valeurs de température inattendues.</span><span class="sxs-lookup"><span data-stu-id="c3690-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="c3690-117">Les sections suivantes vous montrent comment :</span><span class="sxs-lookup"><span data-stu-id="c3690-117">The following sections show you how to:</span></span>

* <span data-ttu-id="c3690-118">identifier les appareils qui envoient des valeurs de température inattendues ;</span><span class="sxs-lookup"><span data-stu-id="c3690-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="c3690-119">configurer ces appareils pour envoyer des données de télémétrie plus détaillées ;</span><span class="sxs-lookup"><span data-stu-id="c3690-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="c3690-120">résoudre le problème en mettant à jour le microprogramme sur ces appareils ;</span><span class="sxs-lookup"><span data-stu-id="c3690-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="c3690-121">vérifier que votre action a résolu le problème.</span><span class="sxs-lookup"><span data-stu-id="c3690-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="c3690-122">Une fonctionnalité clé de ce scénario est que vous pouvez effectuer toutes ces actions à distance à partir du tableau de bord de solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="c3690-123">Vous n’avez pas besoin d’un accès physique aux appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="c3690-124">Afficher le tableau de bord de solution</span><span class="sxs-lookup"><span data-stu-id="c3690-124">View the solution dashboard</span></span>

<span data-ttu-id="c3690-125">Grâce au tableau de bord de solution, vous pouvez gérer la solution déployée.</span><span class="sxs-lookup"><span data-stu-id="c3690-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="c3690-126">Par exemple, vous pouvez afficher les données de télémétrie, ajouter des appareils et configurer des règles.</span><span class="sxs-lookup"><span data-stu-id="c3690-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="c3690-127">Une fois que l’approvisionnement est terminé et que la vignette de votre solution préconfigurée indique **Prêt**, choisissez **Lancer** pour ouvrir le portail de votre solution de surveillance à distance dans un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="c3690-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Lancer la solution préconfigurée][img-launch-solution]

1. <span data-ttu-id="c3690-129">Par défaut, le portail de solution affiche le *tableau de bord*.</span><span class="sxs-lookup"><span data-stu-id="c3690-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="c3690-130">Vous pouvez accéder à d’autres zones du portail de solution à l’aide du menu sur le côté gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="c3690-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Tableau de bord de solution préconfigurée de surveillance à distance][img-menu]

<span data-ttu-id="c3690-132">Le tableau de bord affiche les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c3690-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="c3690-133">Une carte qui affiche l’emplacement de chaque appareil connecté à la solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="c3690-134">Lors de la première exécution de la solution, 25 appareils sont simulés.</span><span class="sxs-lookup"><span data-stu-id="c3690-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="c3690-135">Les appareils simulés sont implémentés en tant qu’Azure WebJobs, et la solution utilise l'API Bing Maps pour tracer les informations sur la carte.</span><span class="sxs-lookup"><span data-stu-id="c3690-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="c3690-136">Consultez le [FAQ][lnk-faq] pour savoir comment rendre le mappage dynamique.</span><span class="sxs-lookup"><span data-stu-id="c3690-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="c3690-137">Un panneau **Historique de télémétrie** qui trace la télémétrie de l’humidité et de la température d’un appareil sélectionné en temps quasi-réel et affiche les données d’agrégation telles que l’humidité maximale, minimale et moyenne.</span><span class="sxs-lookup"><span data-stu-id="c3690-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="c3690-138">Un panneau **Historique des alertes** qui affiche les alarmes récentes lorsqu’une valeur de télémétrie a dépassé un seuil défini.</span><span class="sxs-lookup"><span data-stu-id="c3690-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="c3690-139">Vous pouvez définir vos propres alarmes en plus des exemples créés par la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="c3690-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="c3690-140">Un panneau **Tâches** qui affiche des informations sur les travaux planifiés.</span><span class="sxs-lookup"><span data-stu-id="c3690-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="c3690-141">Vous pouvez planifier vos propres tâches sur la page **Gestion des tâches**.</span><span class="sxs-lookup"><span data-stu-id="c3690-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="c3690-142">Afficher les alarmes</span><span class="sxs-lookup"><span data-stu-id="c3690-142">View alarms</span></span>

<span data-ttu-id="c3690-143">Le panneau Historique des alarmes montre que cinq appareils signalent des valeurs de télémétrie plus élevées que celles attendues.</span><span class="sxs-lookup"><span data-stu-id="c3690-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![TODO Historique des alarmes dans le tableau de bord de solution][img-alarms]

> [!NOTE]
> <span data-ttu-id="c3690-145">Ces alarmes sont générées par une règle qui est incluse dans la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="c3690-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="c3690-146">Cette règle génère une alerte lorsque la valeur de température envoyée par un appareil dépasse 60.</span><span class="sxs-lookup"><span data-stu-id="c3690-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="c3690-147">Vous pouvez définir vos propres règles et actions en choisissant [Règles](#add-a-rule) et [Actions](#add-an-action) dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="c3690-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="c3690-148">Afficher les appareils</span><span class="sxs-lookup"><span data-stu-id="c3690-148">View devices</span></span>

<span data-ttu-id="c3690-149">La liste des *appareils* montre tous les appareils inscrits dans la solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="c3690-150">Dans la liste des appareils, vous pouvez consulter et modifier les métadonnées des appareils, ajouter ou supprimer des appareils et appeler des méthodes sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="c3690-151">Vous pouvez filtrer et trier la liste des appareils dans la liste.</span><span class="sxs-lookup"><span data-stu-id="c3690-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="c3690-152">Vous pouvez également personnaliser les colonnes affichées dans la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="c3690-153">Choisissez **Appareils** pour afficher la liste des appareils pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![Affichage de la liste des appareils dans le portail de solution][img-devicelist]

1. <span data-ttu-id="c3690-155">La liste des appareils montre au départ 25 appareils simulés créés par le processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c3690-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="c3690-156">Vous pouvez ajouter des appareils physiques et simulés supplémentaires à la solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="c3690-157">Pour afficher les détails d’un appareil, choisissez un appareil dans la liste.</span><span class="sxs-lookup"><span data-stu-id="c3690-157">To view the details of a device, choose a device in the device list.</span></span>

   ![Affichage des détails de l’appareil dans le portail de solution][img-devicedetails]

<span data-ttu-id="c3690-159">Le volet **Détails de l’appareil** comprend six sections :</span><span class="sxs-lookup"><span data-stu-id="c3690-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="c3690-160">Un ensemble de liens qui vous permettent de personnaliser l’icône de l’appareil, de désactiver l’appareil, d’ajouter une règle, d’appeler une méthode ou d’envoyer une commande.</span><span class="sxs-lookup"><span data-stu-id="c3690-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="c3690-161">Pour voir une comparaison des commandes (messages appareil-à-cloud) et des méthodes (méthodes directes), consultez [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="c3690-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="c3690-162">La section **Jumeau d’appareil - Balises** vous permet de modifier les valeurs des balises pour l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3690-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="c3690-163">Vous pouvez afficher les valeurs des balises dans la liste des appareils et utiliser les valeurs des balises pour filtrer cette liste.</span><span class="sxs-lookup"><span data-stu-id="c3690-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="c3690-164">La section **Jumeau d’appareil - Propriétés souhaitées** vous permet de définir des valeurs de propriétés qui doivent être envoyées à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3690-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="c3690-165">La section **Jumeau d’appareil - Propriétés signalées** affiche les valeurs de propriétés envoyées par l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3690-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="c3690-166">La section **Propriétés de l’appareil** contient des informations du registre des identités, telles que l’ID de l’appareil et ses clés d’authentification.</span><span class="sxs-lookup"><span data-stu-id="c3690-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="c3690-167">La section **Tâches récentes** inclut des informations sur toutes les tâches qui ont récemment ciblé cet appareil.</span><span class="sxs-lookup"><span data-stu-id="c3690-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="c3690-168">Filtrer la liste des appareils</span><span class="sxs-lookup"><span data-stu-id="c3690-168">Filter the device list</span></span>

<span data-ttu-id="c3690-169">Vous pouvez utiliser un filtre pour afficher uniquement les appareils qui envoient des valeurs de température inattendues.</span><span class="sxs-lookup"><span data-stu-id="c3690-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="c3690-170">La solution préconfigurée de surveillance à distance inclut le filtre **Appareils défectueux** pour afficher les appareils ayant une valeur de température moyenne supérieure à 60.</span><span class="sxs-lookup"><span data-stu-id="c3690-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="c3690-171">Vous pouvez également [créer vos propres filtres](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="c3690-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="c3690-172">Choisissez **Ouvrir un filtre enregistré** pour afficher la liste des filtres disponibles.</span><span class="sxs-lookup"><span data-stu-id="c3690-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="c3690-173">Puis choisissez **Appareils défectueux** pour appliquer le filtre :</span><span class="sxs-lookup"><span data-stu-id="c3690-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Affichage de la liste des filtres][img-unhealthy-filter]

1. <span data-ttu-id="c3690-175">La liste des appareils indique à présent uniquement les appareils ayant une valeur de température moyenne supérieure à 60.</span><span class="sxs-lookup"><span data-stu-id="c3690-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Affichage de la liste des appareils filtrée montrant les appareils défectueux][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="c3690-177">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="c3690-177">Update desired properties</span></span>

<span data-ttu-id="c3690-178">Vous avez désormais identifié un ensemble d’appareils nécessitant une correction.</span><span class="sxs-lookup"><span data-stu-id="c3690-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="c3690-179">Toutefois, vous décidez que la fréquence de données de 15 secondes n’est pas suffisante pour un diagnostic clair du problème.</span><span class="sxs-lookup"><span data-stu-id="c3690-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="c3690-180">La modification de la fréquence de télémétrie à cinq secondes pour vous fournir plus de données permet de mieux diagnostiquer le problème.</span><span class="sxs-lookup"><span data-stu-id="c3690-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="c3690-181">Vous pouvez transmettre cette modification de configuration aux appareils distants à partir du portail de la solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="c3690-182">Vous pouvez effectuer cette modification une fois, évaluer l’impact et ensuite agir en fonction des résultats.</span><span class="sxs-lookup"><span data-stu-id="c3690-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="c3690-183">Procédez comme suit pour exécuter un travail qui modifie la propriété souhaitée **TelemetryInterval** pour les appareils affectés.</span><span class="sxs-lookup"><span data-stu-id="c3690-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="c3690-184">Lorsque les appareils reçoivent la nouvelle valeur de propriété **TelemetryInterval**, ils modifient leur configuration pour envoyer la télémétrie toutes les 5 secondes au lieu de 15 :</span><span class="sxs-lookup"><span data-stu-id="c3690-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="c3690-185">Pendant que vous visualisez la liste des appareils défectueux dans la liste des appareils, choisissez **Planificateur de travaux**, puis **Modifier le jumeau d’appareil**.</span><span class="sxs-lookup"><span data-stu-id="c3690-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="c3690-186">Appelez le travail **Modification de l’intervalle de télémétrie**.</span><span class="sxs-lookup"><span data-stu-id="c3690-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="c3690-187">Modifiez la valeur du nom de la **propriété souhaitée** **desired.Config.TelemetryInterval** à cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="c3690-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="c3690-188">Choisissez **Planification**.</span><span class="sxs-lookup"><span data-stu-id="c3690-188">Choose **Schedule**.</span></span>

    ![Modification de la propriété TelemetryInterval à cinq secondes][img-change-interval]

1. <span data-ttu-id="c3690-190">Vous pouvez surveiller la progression du travail sur la page **Gestion des tâches** du portail.</span><span class="sxs-lookup"><span data-stu-id="c3690-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="c3690-191">Si vous souhaitez modifier une valeur de propriété souhaitée pour un appareil en particulier, utilisez la section **Propriétés souhaitées** dans le panneau **Détails de l’appareil** au lieu d’exécuter un travail.</span><span class="sxs-lookup"><span data-stu-id="c3690-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="c3690-192">Ce travail définit la valeur de la propriété souhaitée **TelemetryInterval** dans le jumeau d’appareil pour tous les appareils sélectionnés par le filtre.</span><span class="sxs-lookup"><span data-stu-id="c3690-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="c3690-193">Les appareils extraient cette valeur du jumeau d’appareil et mettent à jour leur comportement.</span><span class="sxs-lookup"><span data-stu-id="c3690-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="c3690-194">Lorsqu’un appareil récupère et traite une propriété souhaitée à partir d’un jumeau d’appareil, il définit la propriété de la valeur signalée correspondante.</span><span class="sxs-lookup"><span data-stu-id="c3690-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="c3690-195">Appeler des méthodes</span><span class="sxs-lookup"><span data-stu-id="c3690-195">Invoke methods</span></span>

<span data-ttu-id="c3690-196">Pendant l’exécution du travail, vous remarquez dans la liste des appareils défectueux que tous ces appareils possèdent une version ancienne de microprogramme (antérieur à la version 1.6).</span><span class="sxs-lookup"><span data-stu-id="c3690-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Affichage de la version du microprogramme signalée pour les appareils défectueux][img-old-firmware]

<span data-ttu-id="c3690-198">Cette version du microprogramme peut être la cause de valeurs de température inattendues, car vous savez que d’autres appareils sains ont récemment été mis à jour vers la version 2.0.</span><span class="sxs-lookup"><span data-stu-id="c3690-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="c3690-199">Vous pouvez utiliser le filtre **Appareils avec ancien microprogramme** pour identifier tous les appareils dotés d’anciennes versions du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="c3690-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="c3690-200">À partir du portail, vous pouvez ensuite mettre à jour à distance tous les appareils exécutant toujours d’anciennes versions du microprogramme :</span><span class="sxs-lookup"><span data-stu-id="c3690-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="c3690-201">Choisissez **Ouvrir un filtre enregistré** pour afficher la liste des filtres disponibles.</span><span class="sxs-lookup"><span data-stu-id="c3690-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="c3690-202">Puis choisissez **Appareils avec ancien microprogramme** pour appliquer le filtre :</span><span class="sxs-lookup"><span data-stu-id="c3690-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Affichage de la liste des filtres][img-old-filter]

1. <span data-ttu-id="c3690-204">La liste des appareils indique à présent uniquement les appareils avec d’anciennes versions du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="c3690-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="c3690-205">Cette liste inclut les cinq appareils identifiés par le filtre **Appareils défectueux** et trois appareils supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="c3690-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![Affichage de la liste des appareils filtrée montrant les anciens appareils][img-filtered-old-list]

1. <span data-ttu-id="c3690-207">Choisissez **Planificateur de travaux**, puis **Appeler une méthode**.</span><span class="sxs-lookup"><span data-stu-id="c3690-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="c3690-208">Définissez le **Nom du travail** sur **Mise à jour du microprogramme vers la version 2.0**.</span><span class="sxs-lookup"><span data-stu-id="c3690-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="c3690-209">Choisissez **InitiateFirmwareUpdate** comme **méthode**.</span><span class="sxs-lookup"><span data-stu-id="c3690-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="c3690-210">Définissez le paramètre **FwPackageUri** sur **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="c3690-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="c3690-211">Choisissez **Planification**.</span><span class="sxs-lookup"><span data-stu-id="c3690-211">Choose **Schedule**.</span></span> <span data-ttu-id="c3690-212">La valeur par défaut pour le travail est une exécution immédiate.</span><span class="sxs-lookup"><span data-stu-id="c3690-212">The default is for the job to run now.</span></span>

    ![Création de travail pour mettre à jour le microprogramme des appareils sélectionnés][img-method-update]

> [!NOTE]
> <span data-ttu-id="c3690-214">Si vous souhaitez appeler une méthode sur un appareil en particulier, choisissez **Méthodes** dans le panneau **Détails de l’appareil** au lieu d’exécuter un travail.</span><span class="sxs-lookup"><span data-stu-id="c3690-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="c3690-215">Ce travail appelle la méthode directe **InitiateFirmwareUpdate** sur tous les appareils sélectionnés par le filtre.</span><span class="sxs-lookup"><span data-stu-id="c3690-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="c3690-216">Les appareils répondent immédiatement à IoT Hub puis lancent le processus de mise à jour du microprogramme de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="c3690-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="c3690-217">Les appareils fournissent des informations d’état sur le processus de mise à jour du microprogramme via les valeurs de propriété signalées, comme indiqué dans les captures d’écran suivantes.</span><span class="sxs-lookup"><span data-stu-id="c3690-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="c3690-218">Choisissez l’icône **Actualiser** pour mettre à jour les informations dans les listes d’appareils et de travaux :</span><span class="sxs-lookup"><span data-stu-id="c3690-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="c3690-219">![Liste de travaux affichant la liste de mises à jour de microprogramme en cours d’exécution][img-update-1]
![Liste des appareils affichant l’état de mise à jour du microprogramme][img-update-2]
![Liste de travaux montrant la liste de mise à jour de microprogramme terminée][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="c3690-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="c3690-220">Dans un environnement de production, vous pouvez planifier des travaux à exécuter pendant une fenêtre de maintenance désignée.</span><span class="sxs-lookup"><span data-stu-id="c3690-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="c3690-221">Analyse du scénario</span><span class="sxs-lookup"><span data-stu-id="c3690-221">Scenario review</span></span>

<span data-ttu-id="c3690-222">Dans ce scénario, vous avez identifié un problème potentiel avec certains de vos appareils à distance à l’aide de l’historique des alarmes sur le tableau de bord et d’un filtre.</span><span class="sxs-lookup"><span data-stu-id="c3690-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="c3690-223">Vous avez ensuite utilisé le filtre et un travail pour configurer à distance les appareils pour fournir plus d’informations pour vous aider à diagnostiquer le problème.</span><span class="sxs-lookup"><span data-stu-id="c3690-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="c3690-224">Enfin, vous avez utilisé un filtre et un travail pour planifier la maintenance sur les appareils affectés.</span><span class="sxs-lookup"><span data-stu-id="c3690-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="c3690-225">Si vous retournez au tableau de bord, vous pouvez vérifier qu’il ne reste aucune alarme provenant des appareils de votre solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="c3690-226">Vous pouvez utiliser un filtre pour vérifier que le microprogramme est à jour sur tous les appareils de votre solution et qu’il ne reste aucun appareil défectueux :</span><span class="sxs-lookup"><span data-stu-id="c3690-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtre indiquant que tous les appareils disposent d’un microprogramme à jour][img-updated]

![Filtre indiquant que tous les appareils sont sains][img-healthy]

## <a name="other-features"></a><span data-ttu-id="c3690-229">Autres fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="c3690-229">Other features</span></span>

<span data-ttu-id="c3690-230">Les sections suivantes décrivent quelques fonctionnalités supplémentaires de la solution préconfigurée de surveillance à distance qui ne sont pas décrites dans le cadre du scénario précédent.</span><span class="sxs-lookup"><span data-stu-id="c3690-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="c3690-231">Personnaliser les colonnes</span><span class="sxs-lookup"><span data-stu-id="c3690-231">Customize columns</span></span>

<span data-ttu-id="c3690-232">Vous pouvez personnaliser les informations affichées dans la liste des appareils en choisissant **Éditeur de colonne**.</span><span class="sxs-lookup"><span data-stu-id="c3690-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="c3690-233">Vous pouvez ajouter et supprimer des colonnes dans lesquelles figurent des valeurs de balises et de propriétés signalées.</span><span class="sxs-lookup"><span data-stu-id="c3690-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="c3690-234">Vous pouvez également réorganiser et renommer les colonnes :</span><span class="sxs-lookup"><span data-stu-id="c3690-234">You can also reorder and rename columns:</span></span>

   ![Icône de l’éditeur de colonne dans la liste des appareils][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="c3690-236">Personnaliser l’icône de l’appareil</span><span class="sxs-lookup"><span data-stu-id="c3690-236">Customize the device icon</span></span>

<span data-ttu-id="c3690-237">Vous pouvez personnaliser l’icône de l’appareil qui apparaît dans la liste des appareils à partir du volet **Détails de l’appareil**, en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3690-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="c3690-238">Choisissez l’icône représentant un crayon pour ouvrir le volet **Modifier une image** pour un appareil :</span><span class="sxs-lookup"><span data-stu-id="c3690-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Ouvrir l’éditeur d’image d’appareil][img-startimageedit]

1. <span data-ttu-id="c3690-240">Téléchargez une nouvelle image ou utilisez une image existante, puis choisissez **Enregistrer** :</span><span class="sxs-lookup"><span data-stu-id="c3690-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Modifier l’éditeur d’image d’appareil][img-imageedit]

1. <span data-ttu-id="c3690-242">L’image que vous avez sélectionnée s’affiche dans la colonne **Icône** de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3690-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="c3690-243">L’image est enregistrée dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="c3690-243">The image is stored in blob storage.</span></span> <span data-ttu-id="c3690-244">Une balise du jumeau d’appareil contient un lien vers l’image dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="c3690-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="c3690-245">Ajout d’un appareil</span><span class="sxs-lookup"><span data-stu-id="c3690-245">Add a device</span></span>

<span data-ttu-id="c3690-246">Lorsque vous déployez la solution préconfigurée, vous approvisionnez automatiquement 25 exemples d’appareils que vous pouvez voir dans la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="c3690-247">Ces appareils sont des *simulations d’appareils* en cours d’exécution dans un Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="c3690-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="c3690-248">Les appareils simulés vous permettent d’expérimenter plus facilement la solution préconfigurée sans avoir à déployer des appareils physiques réels.</span><span class="sxs-lookup"><span data-stu-id="c3690-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="c3690-249">Si vous ne souhaitez pas connecter un appareil physique à la solution, consultez le didacticiel [Connexion de votre appareil à la solution préconfigurée de surveillance à distance][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="c3690-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="c3690-250">Les étapes suivantes vous montrent comment ajouter un appareil simulé à la solution :</span><span class="sxs-lookup"><span data-stu-id="c3690-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="c3690-251">Retournez à la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="c3690-252">Pour ajouter un appareil, choisissez **+ Ajouter un appareil** dans le coin inférieur gauche.</span><span class="sxs-lookup"><span data-stu-id="c3690-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Ajouter un appareil à la solution préconfigurée][img-adddevice]

1. <span data-ttu-id="c3690-254">Choisissez **Ajouter un nouveau** sur la vignette **Appareil simulé**.</span><span class="sxs-lookup"><span data-stu-id="c3690-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Définir les détails du nouvel appareil dans le tableau de bord][img-addnew]

   <span data-ttu-id="c3690-256">Outre la création d’un appareil simulé, vous pouvez également ajouter un appareil physique si vous choisissez de créer un **appareil personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="c3690-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="c3690-257">Pour plus d’informations sur la connexion d’appareils physiques à la solution, consultez [Connexion de votre appareil à la solution préconfigurée de surveillance à distance][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="c3690-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="c3690-258">Sélectionnez **Me laisser définir mon propre ID d’appareil** et ajoutez un nom unique d’ID d’appareil, par exemple **monappareil_01**.</span><span class="sxs-lookup"><span data-stu-id="c3690-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="c3690-259">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c3690-259">Choose **Create**.</span></span>

   ![Enregistrer un nouvel appareil][img-definedevice]

1. <span data-ttu-id="c3690-261">À l’étape 3 de la procédure **Ajouter un appareil simulé**, choisissez **Terminé** pour revenir à la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="c3690-262">Vous pouvez vérifier que votre appareil est **En cours d’exécution** dans la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-262">You can view your device **Running** in the device list.</span></span>

    ![Afficher le nouvel appareil dans la liste des appareils][img-runningnew]

1. <span data-ttu-id="c3690-264">Vous pouvez également afficher les données de télémétrie provenant de votre nouvel appareil sur le tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="c3690-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![Afficher la télémétrie du nouvel appareil][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="c3690-266">Désactiver et supprimer un appareil</span><span class="sxs-lookup"><span data-stu-id="c3690-266">Disable and delete a device</span></span>

<span data-ttu-id="c3690-267">Vous pouvez désactiver un appareil puis le supprimer :</span><span class="sxs-lookup"><span data-stu-id="c3690-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Désactiver et supprimer un appareil][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="c3690-269">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="c3690-269">Add a rule</span></span>

<span data-ttu-id="c3690-270">Il n'existe aucune règle pour le nouvel appareil que vous venez d'ajouter.</span><span class="sxs-lookup"><span data-stu-id="c3690-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="c3690-271">Dans cette section, vous allez ajouter une règle qui déclenche une alarme lorsque la température signalée par le nouvel appareil dépasse 47 degrés.</span><span class="sxs-lookup"><span data-stu-id="c3690-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="c3690-272">Avant de commencer, notez que l'historique de télémétrie pour le nouvel appareil sur le tableau de bord affiche que la température de l’appareil ne dépasse jamais 45 degrés.</span><span class="sxs-lookup"><span data-stu-id="c3690-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="c3690-273">Retournez à la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="c3690-274">Pour ajouter une règle concernant un nouvel appareil, sélectionnez ce dernier dans la **liste des appareils**, puis choisissez **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="c3690-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="c3690-275">Créez une règle qui utilise **Température** comme champ de données et **AlarmTemp** en tant que sortie lorsque la température dépasse 47 degrés :</span><span class="sxs-lookup"><span data-stu-id="c3690-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule]

1. <span data-ttu-id="c3690-277">Pour enregistrer vos modifications, choisissez **Enregistrer et afficher les règles**.</span><span class="sxs-lookup"><span data-stu-id="c3690-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="c3690-278">Choisissez **Commandes** dans le volet Détails du nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="c3690-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule2]

1. <span data-ttu-id="c3690-280">Sélectionnez **ChangeSetPointTemp** dans la liste de commandes et définissez **SetPointTemp** sur 45.</span><span class="sxs-lookup"><span data-stu-id="c3690-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="c3690-281">Puis choisissez **Envoyer la commande** :</span><span class="sxs-lookup"><span data-stu-id="c3690-281">Then choose **Send Command**:</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule3]

1. <span data-ttu-id="c3690-283">Revenez au tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="c3690-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="c3690-284">Rapidement s’affiche une nouvelle entrée dans le volet **Historique des alarmes** , lorsque la température signalée par votre nouvel appareil dépasse le seuil de 47 degrés :</span><span class="sxs-lookup"><span data-stu-id="c3690-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Ajouter une règle d’appareil][img-adddevicerule4]

1. <span data-ttu-id="c3690-286">Vous pouvez consulter et modifier toutes les règles dans le tableau de bord **Règles** :</span><span class="sxs-lookup"><span data-stu-id="c3690-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![Répertorier les règles d’appareil][img-rules]

1. <span data-ttu-id="c3690-288">Vous pouvez consulter et modifier toutes les mesures qui peuvent être prises en réponse à une règle sur le tableau de bord **Actions** :</span><span class="sxs-lookup"><span data-stu-id="c3690-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![Répertorier les actions d’appareil][img-actions]

> [!NOTE]
> <span data-ttu-id="c3690-290">Il est possible de définir des actions pouvant envoyer un message électronique ou un SMS en réponse à une règle ou s’intégrer à un système métier par le biais d’une [application logique][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="c3690-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="c3690-291">Pour plus d’informations consultez [Connecter Logic App à la solution préconfigurée de surveillance à distance IoT Suite][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="c3690-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="c3690-292">Gérer les filtres</span><span class="sxs-lookup"><span data-stu-id="c3690-292">Manage filters</span></span>

<span data-ttu-id="c3690-293">Dans la liste des appareils, vous pouvez créer, enregistrer et recharger des filtres pour afficher une liste personnalisée des appareils connectés à votre hub.</span><span class="sxs-lookup"><span data-stu-id="c3690-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="c3690-294">Pour créer un filtre :</span><span class="sxs-lookup"><span data-stu-id="c3690-294">To create a filter:</span></span>

1. <span data-ttu-id="c3690-295">Choisissez l’icône de modification de filtre au-dessus de la liste des appareils :</span><span class="sxs-lookup"><span data-stu-id="c3690-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Ouvrir l’éditeur de filtre][img-editfiltericon]

1. <span data-ttu-id="c3690-297">Dans l’**éditeur de filtre**, ajoutez les champs, les opérateurs et les valeurs permettant de filtrer la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="c3690-298">Vous pouvez ajouter plusieurs clauses pour affiner votre filtre.</span><span class="sxs-lookup"><span data-stu-id="c3690-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="c3690-299">Choisissez **Filtrer** pour appliquer le filtre :</span><span class="sxs-lookup"><span data-stu-id="c3690-299">Choose **Filter** to apply the filter:</span></span>

    ![Créer un filtre][img-filtereditor]

1. <span data-ttu-id="c3690-301">Dans cet exemple, la liste est filtrée par fabricant et numéro de modèle :</span><span class="sxs-lookup"><span data-stu-id="c3690-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Liste de filtrage][img-filterelist]

1. <span data-ttu-id="c3690-303">Pour enregistrer votre filtre avec un nom personnalisé, choisissez l’icône **Enregistrer sous** :</span><span class="sxs-lookup"><span data-stu-id="c3690-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Enregistrer un filtre][img-savefilter]

1. <span data-ttu-id="c3690-305">Pour réappliquer un filtre que vous avez enregistré précédemment, choisissez l’icône **Ouvrir un filtre enregistré** :</span><span class="sxs-lookup"><span data-stu-id="c3690-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Ouvrir un filtre][img-openfilter]

<span data-ttu-id="c3690-307">Vous pouvez créer des filtres en fonction de l’id de l’appareil, de son état, des propriétés souhaitées, des propriétés signalées et des balises.</span><span class="sxs-lookup"><span data-stu-id="c3690-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="c3690-308">Vous ajoutez vos propres balises personnalisées à un appareil dans la section **Balises** du panneau **Détails de l’appareil** ou exécutez un travail pour mettre à jour les balises sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="c3690-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="c3690-309">Dans l’**éditeur de filtre**, vous pouvez utiliser la **vue avancée** pour modifier directement le texte de la requête.</span><span class="sxs-lookup"><span data-stu-id="c3690-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="c3690-310">Commandes</span><span class="sxs-lookup"><span data-stu-id="c3690-310">Commands</span></span>

<span data-ttu-id="c3690-311">Dans le volet **Détails de l’appareil**, vous pouvez envoyer des commandes à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3690-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="c3690-312">Lors du premier démarrage d'un appareil, ce dernier envoie des informations sur les commandes qu'il prend en charge à la solution.</span><span class="sxs-lookup"><span data-stu-id="c3690-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="c3690-313">Pour une explication des différences entre les commandes et les méthodes, consultez [Options cloud vers appareil Azure IoT Hub][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="c3690-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="c3690-314">Choisissez **Commandes** dans le panneau **Détails de l’appareil** correspondant à l’appareil sélectionné :</span><span class="sxs-lookup"><span data-stu-id="c3690-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Commandes de l’appareil dans le tableau de bord][img-devicecommands]

1. <span data-ttu-id="c3690-316">Sélectionnez **PingDevice** dans la liste de commandes.</span><span class="sxs-lookup"><span data-stu-id="c3690-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="c3690-317">Choisissez **Envoyer la commande**.</span><span class="sxs-lookup"><span data-stu-id="c3690-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="c3690-318">Vous pouvez visualiser l’état de la commande dans l’historique des commandes.</span><span class="sxs-lookup"><span data-stu-id="c3690-318">You can see the status of the command in the command history.</span></span>

   ![État de la commande dans le tableau de bord][img-pingcommand]

<span data-ttu-id="c3690-320">La solution effectue le suivi de l'état de chaque commande qu'elle envoie.</span><span class="sxs-lookup"><span data-stu-id="c3690-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="c3690-321">Initialement, le résultat est **En attente**.</span><span class="sxs-lookup"><span data-stu-id="c3690-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="c3690-322">Lorsque l’appareil signale qu’il a correctement exécuté la commande, le résultat prend la valeur **Réussite**.</span><span class="sxs-lookup"><span data-stu-id="c3690-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="c3690-323">Dans les coulisses</span><span class="sxs-lookup"><span data-stu-id="c3690-323">Behind the scenes</span></span>

<span data-ttu-id="c3690-324">Lorsque vous déployez une solution préconfigurée, le processus de déploiement crée plusieurs ressources dans l’abonnement Azure sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c3690-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="c3690-325">Vous pouvez afficher ces ressources dans le [portail][lnk-portal] Azure.</span><span class="sxs-lookup"><span data-stu-id="c3690-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="c3690-326">Le processus de déploiement crée un **groupe de ressources** avec un nom basé sur celui que vous avez choisi pour votre solution préconfigurée :</span><span class="sxs-lookup"><span data-stu-id="c3690-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Solution préconfigurée dans le portail Azure][img-portal]

<span data-ttu-id="c3690-328">Vous pouvez afficher les paramètres de chaque ressource en la sélectionnant dans la liste des ressources dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c3690-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="c3690-329">Vous pouvez également afficher le code source pour la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="c3690-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="c3690-330">Le code source de la solution préconfigurée de surveillance à distance se trouve dans le référentiel GitHub [azure-iot-remote-monitoring][lnk-rmgithub] :</span><span class="sxs-lookup"><span data-stu-id="c3690-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="c3690-331">Le dossier **DeviceAdministration** contient le code source pour le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="c3690-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="c3690-332">Le dossier **Simulator** contient le code source pour l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="c3690-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="c3690-333">Le dossier **EventProcessor** contient le code source pour le processus principal qui gère les données de télémétrie entrantes.</span><span class="sxs-lookup"><span data-stu-id="c3690-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="c3690-334">Lorsque vous avez terminé, vous pouvez supprimer la solution préconfigurée à partir de votre abonnement Azure sur le site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="c3690-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="c3690-335">Ce site vous permet de supprimer facilement toutes les ressources qui ont été configurées lors de la création de la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="c3690-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="c3690-336">Pour vous assurer que vous supprimez tout ce qui concerne la solution préconfigurée, supprimez cette dernière sur le site [azureiotsuite.com][lnk-azureiotsuite] ; ne supprimez pas le groupe de ressources dans le portail.</span><span class="sxs-lookup"><span data-stu-id="c3690-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3690-337">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3690-337">Next Steps</span></span>

<span data-ttu-id="c3690-338">À présent que vous avez déployé une solution préconfigurée opérationnelle, vous pouvez poursuivre la prise en main d’IoT Suite en lisant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="c3690-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="c3690-339">[Présentation de la solution préconfigurée de surveillance à distance][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="c3690-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="c3690-340">[Connexion de votre appareil à la solution préconfigurée de surveillance à distance][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="c3690-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="c3690-341">[Autorisations sur le site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="c3690-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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