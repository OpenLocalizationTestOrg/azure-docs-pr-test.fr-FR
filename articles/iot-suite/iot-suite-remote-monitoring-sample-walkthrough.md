---
title: "procédure pas à pas solution d’analyse préconfiguré aaaRemote | Documents Microsoft"
description: "Obtenir une description de hello Azure IoT préconfiguré son architecture et surveillance à distance de la solution."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="57aab-103">Présentation de la solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="57aab-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="57aab-104">Hello surveillance à distance IoT Suite [solution préconfigurée] [ lnk-preconfigured-solutions] est une implémentation d’un bout à bout surveillance des solutions pour plusieurs ordinateurs en cours d’exécution dans des emplacements distants.</span><span class="sxs-lookup"><span data-stu-id="57aab-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="57aab-105">solution de Hello associe des principaux services Azure tooprovide une implémentation générique de scénario d’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="57aab-106">Vous pouvez utiliser la solution de hello comme point de départ pour votre propre implémentation et [personnaliser] [ lnk-customize] il toomeet vos propres besoins professionnels spécifiques.</span><span class="sxs-lookup"><span data-stu-id="57aab-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="57aab-107">Cet article vous guide certains éléments clés hello tooenable de solution d’analyse à distance hello toounderstand son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="57aab-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="57aab-108">Ces connaissances vous aident à :</span><span class="sxs-lookup"><span data-stu-id="57aab-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="57aab-109">Résoudre les problèmes dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="57aab-110">Planifier comment toocustomize toohello solution toomeet vos besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="57aab-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="57aab-111">Concevoir votre propre solution IoT utilisant des services Azure.</span><span class="sxs-lookup"><span data-stu-id="57aab-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="57aab-112">Architecture logique</span><span class="sxs-lookup"><span data-stu-id="57aab-112">Logical architecture</span></span>

<span data-ttu-id="57aab-113">Hello suivant schéma présente des composants logiques de hello de solution de hello préconfiguré :</span><span class="sxs-lookup"><span data-stu-id="57aab-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Architecture logique](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="57aab-115">Simulations d’appareils</span><span class="sxs-lookup"><span data-stu-id="57aab-115">Simulated devices</span></span>

<span data-ttu-id="57aab-116">Dans la solution de hello préconfiguré, appareil simulé de hello représente un périphérique de refroidissement (comme un bâtiment climatisation ou l’unité de gestion des installations air).</span><span class="sxs-lookup"><span data-stu-id="57aab-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="57aab-117">Lorsque vous déployez la solution de hello préconfiguré, vous déployez également automatiquement quatre périphériques simulés qui s’exécutent dans un [la tâche Web Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="57aab-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="57aab-118">les appareils Hello simulée facilitent vous tooexplore hello comportement de hello solution sans hello besoin toodeploy tous les périphériques physiques.</span><span class="sxs-lookup"><span data-stu-id="57aab-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="57aab-119">toodeploy un appareil physique réel, consultez hello [connecter votre solution préconfigurée de surveillance à distance de toohello périphérique] [ lnk-connect-rm] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="57aab-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="57aab-120">Messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="57aab-120">Device-to-cloud messages</span></span>

<span data-ttu-id="57aab-121">Chaque appareil simulé peut envoyer hello suivant les types de message tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="57aab-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="57aab-122">Message</span><span class="sxs-lookup"><span data-stu-id="57aab-122">Message</span></span> | <span data-ttu-id="57aab-123">Description</span><span class="sxs-lookup"><span data-stu-id="57aab-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57aab-124">Démarrage</span><span class="sxs-lookup"><span data-stu-id="57aab-124">Startup</span></span> |<span data-ttu-id="57aab-125">Lorsque le périphérique de hello démarre, il envoie un **informations de périphérique** message contenant des informations sur lui-même toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="57aab-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="57aab-126">Ces données incluent l’id de périphérique hello et une liste des commandes hello et méthodes hello périphérique prend en charge.</span><span class="sxs-lookup"><span data-stu-id="57aab-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="57aab-127">Présence</span><span class="sxs-lookup"><span data-stu-id="57aab-127">Presence</span></span> |<span data-ttu-id="57aab-128">Un périphérique envoie régulièrement un **présence** tooreport de message si l’appareil de hello peut détecter la présence hello d’un capteur.</span><span class="sxs-lookup"><span data-stu-id="57aab-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="57aab-129">Télémétrie</span><span class="sxs-lookup"><span data-stu-id="57aab-129">Telemetry</span></span> |<span data-ttu-id="57aab-130">Un périphérique envoie régulièrement un **télémétrie** message qui affiche les valeurs de température de hello et de l’humidité collectées à partir de l’appareil de hello simulés de simulée capteurs.</span><span class="sxs-lookup"><span data-stu-id="57aab-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="57aab-131">solution de Hello stocke la liste hello des commandes prises en charge par le périphérique hello dans une base de données de la base de données Cosmos et non en double d’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="57aab-132">Propriétés et représentations d’appareil</span><span class="sxs-lookup"><span data-stu-id="57aab-132">Properties and device twins</span></span>

<span data-ttu-id="57aab-133">Hello simulés périphériques les envoient hello suivant appareil propriétés toohello [double] [ lnk-device-twins] dans hello IoT hub en tant que *signalé propriétés*.</span><span class="sxs-lookup"><span data-stu-id="57aab-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="57aab-134">Hello envoie de périphérique signalé propriétés au démarrage et dans la réponse tooa **changement d’état appareil** commande ou la méthode.</span><span class="sxs-lookup"><span data-stu-id="57aab-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="57aab-135">Propriété</span><span class="sxs-lookup"><span data-stu-id="57aab-135">Property</span></span> | <span data-ttu-id="57aab-136">Objectif</span><span class="sxs-lookup"><span data-stu-id="57aab-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="57aab-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="57aab-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="57aab-138">L’unité de fréquence (secondes) hello envoie des données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="57aab-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="57aab-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="57aab-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="57aab-140">Spécifie la valeur moyenne de hello de télémétrie de température hello simulé</span><span class="sxs-lookup"><span data-stu-id="57aab-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="57aab-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="57aab-141">Device.DeviceID</span></span> |<span data-ttu-id="57aab-142">ID qui est fourni ou affecté lors de la création d’une unité dans la solution de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="57aab-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="57aab-143">Device.DeviceState</span></span> | <span data-ttu-id="57aab-144">État signalée par le périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-144">State reported by hello device</span></span> |
| <span data-ttu-id="57aab-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="57aab-145">Device.CreatedTime</span></span> |<span data-ttu-id="57aab-146">APPAREIL hello a été créé dans la solution de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="57aab-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="57aab-147">Device.StartupTime</span></span> |<span data-ttu-id="57aab-148">APPAREIL hello a été démarré.</span><span class="sxs-lookup"><span data-stu-id="57aab-148">Time hello device was started</span></span> |
| <span data-ttu-id="57aab-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="57aab-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="57aab-150">numéro de version Hello de propriété désirée de hello dernière modification</span><span class="sxs-lookup"><span data-stu-id="57aab-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="57aab-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="57aab-151">Device.Location.Latitude</span></span> |<span data-ttu-id="57aab-152">Emplacement de latitude de l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="57aab-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="57aab-153">Device.Location.Longitude</span></span> |<span data-ttu-id="57aab-154">Emplacement de longitude de l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="57aab-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="57aab-155">System.Manufacturer</span></span> |<span data-ttu-id="57aab-156">Fabricant de l'appareil</span><span class="sxs-lookup"><span data-stu-id="57aab-156">Device manufacturer</span></span> |
| <span data-ttu-id="57aab-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="57aab-157">System.ModelNumber</span></span> |<span data-ttu-id="57aab-158">Numéro de modèle du périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-158">Model number of hello device</span></span> |
| <span data-ttu-id="57aab-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="57aab-159">System.SerialNumber</span></span> |<span data-ttu-id="57aab-160">Numéro de série du périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-160">Serial number of hello device</span></span> |
| <span data-ttu-id="57aab-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="57aab-161">System.FirmwareVersion</span></span> |<span data-ttu-id="57aab-162">Version actuelle du microprogramme sur l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="57aab-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="57aab-163">System.Platform</span></span> |<span data-ttu-id="57aab-164">Architecture de la plate-forme de périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="57aab-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="57aab-165">System.Processor</span></span> |<span data-ttu-id="57aab-166">Périphérique hello en cours d’exécution de processeur</span><span class="sxs-lookup"><span data-stu-id="57aab-166">Processor running hello device</span></span> |
| <span data-ttu-id="57aab-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="57aab-167">System.InstalledRAM</span></span> |<span data-ttu-id="57aab-168">Quantité de RAM installée sur l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="57aab-169">Simulateur de Hello amorce ces propriétés dans les périphériques simulés avec des exemples de valeurs.</span><span class="sxs-lookup"><span data-stu-id="57aab-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="57aab-170">Chaque fois que simulateur de hello Initialise un appareil simulé, l’appareil de hello signale hello métadonnées prédéfinies tooIoT Hub en tant que propriétés déclarées.</span><span class="sxs-lookup"><span data-stu-id="57aab-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="57aab-171">Propriétés déclarées peuvent uniquement être mis à jour par périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="57aab-172">toochange une propriété signalée, vous permet de définir une propriété de votre choix dans le portail de la solution.</span><span class="sxs-lookup"><span data-stu-id="57aab-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="57aab-173">Il incombe hello du périphérique hello pour :</span><span class="sxs-lookup"><span data-stu-id="57aab-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="57aab-174">Extraire périodiquement des propriétés souhaitées à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="57aab-175">Mettre à jour sa configuration avec la valeur de la propriété hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="57aab-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="57aab-176">Envoyer le nouveau concentrateur de retour toohello valeur hello comme propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="57aab-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="57aab-177">À partir du tableau de bord hello solution, vous pouvez utiliser *propriétés souhaitée* tooset des propriétés sur un périphérique à l’aide de hello [double de l’appareil][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="57aab-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="57aab-178">En règle générale, un appareil lit une valeur de propriété souhaitée tooupdate de concentrateur hello que son état interne et le hello du rapport modifier comme une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="57aab-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="57aab-179">Hello appareil simulé code utilise uniquement hello **Desired.Config.TemperatureMeanValue** et **Desired.Config.TelemetryInterval** hello tooupdate de propriétés souhaitées signalé a renvoyé des propriétés tooIoT concentrateur.</span><span class="sxs-lookup"><span data-stu-id="57aab-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="57aab-180">Toutes les autres demandes de modification de propriété de votre choix sont ignorés dans les appareil simulé hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="57aab-181">Méthodes</span><span class="sxs-lookup"><span data-stu-id="57aab-181">Methods</span></span>

<span data-ttu-id="57aab-182">Hello simulés appareils peuvent gérer hello méthodes suivantes ([direct de méthodes][lnk-direct-methods]) à partir du portail de solution hello via IoT hub de hello appelé :</span><span class="sxs-lookup"><span data-stu-id="57aab-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="57aab-183">Méthode</span><span class="sxs-lookup"><span data-stu-id="57aab-183">Method</span></span> | <span data-ttu-id="57aab-184">Description</span><span class="sxs-lookup"><span data-stu-id="57aab-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57aab-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="57aab-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="57aab-186">Fait en sorte que hello appareil tooperform une mise à jour du microprogramme</span><span class="sxs-lookup"><span data-stu-id="57aab-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="57aab-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="57aab-187">Reboot</span></span> |<span data-ttu-id="57aab-188">Fait en sorte que hello appareil tooreboot</span><span class="sxs-lookup"><span data-stu-id="57aab-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="57aab-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="57aab-189">FactoryReset</span></span> |<span data-ttu-id="57aab-190">Fait en sorte que tooperform de périphérique hello une réinitialisation</span><span class="sxs-lookup"><span data-stu-id="57aab-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="57aab-191">Certaines méthodes utilisent des propriétés déclarées tooreport sur la progression.</span><span class="sxs-lookup"><span data-stu-id="57aab-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="57aab-192">Par exemple, hello **InitiateFirmwareUpdate** méthode simule la mise à jour de hello en cours d’exécution en mode asynchrone sur le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="57aab-193">méthode Hello retourne immédiatement sur le périphérique de hello, sans interrompre la tâche asynchrone hello toosend état mises à jour à l’aide du tableau de bord de solution toohello signalé propriétés.</span><span class="sxs-lookup"><span data-stu-id="57aab-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="57aab-194">Commandes</span><span class="sxs-lookup"><span data-stu-id="57aab-194">Commands</span></span>

<span data-ttu-id="57aab-195">les appareils Hello simulée peuvent gérer hello suivant les commandes (messages cloud-à-appareil) envoyés à partir du portail de solution hello via IoT hub de hello :</span><span class="sxs-lookup"><span data-stu-id="57aab-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="57aab-196">Commande</span><span class="sxs-lookup"><span data-stu-id="57aab-196">Command</span></span> | <span data-ttu-id="57aab-197">Description</span><span class="sxs-lookup"><span data-stu-id="57aab-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57aab-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="57aab-198">PingDevice</span></span> |<span data-ttu-id="57aab-199">Envoie un *ping* toocheck de périphérique toohello il est actif</span><span class="sxs-lookup"><span data-stu-id="57aab-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="57aab-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="57aab-200">StartTelemetry</span></span> |<span data-ttu-id="57aab-201">Appareil de hello démarre l’envoi de données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="57aab-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="57aab-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="57aab-202">StopTelemetry</span></span> |<span data-ttu-id="57aab-203">Appareil de hello cesse d’envoyer des données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="57aab-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="57aab-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="57aab-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="57aab-205">Valeur de définir le point de hello modifications quels hello autour des données aléatoires sont générées</span><span class="sxs-lookup"><span data-stu-id="57aab-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="57aab-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="57aab-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="57aab-207">Déclencheurs hello toosend de simulateur d’appareil une valeur de télémétrie supplémentaires (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="57aab-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="57aab-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="57aab-208">ChangeDeviceState</span></span> |<span data-ttu-id="57aab-209">Modifie une propriété de l’état étendu pour appareil de hello et envoie un message d’information d’appareil hello à partir de l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="57aab-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="57aab-210">Pour voir une comparaison de ces commandes (cloud-à-appareil) et des méthodes (méthodes directes), consultez [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="57aab-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="57aab-211">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="57aab-211">IoT Hub</span></span>

<span data-ttu-id="57aab-212">Hello [IoT hub] [ lnk-iothub] reçoit les données envoyées à partir d’appareils de hello dans le cloud de hello et rend les travaux d’Analytique de flux de données Azure (ASA) toohello disponibles.</span><span class="sxs-lookup"><span data-stu-id="57aab-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="57aab-213">Chaque travail ASA de flux de données utilise un flux d’hello de tooread IoT Hub consommateur groupe distinct des messages à partir de vos appareils.</span><span class="sxs-lookup"><span data-stu-id="57aab-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="57aab-214">Hello IoT hub dans les solutions hello également :</span><span class="sxs-lookup"><span data-stu-id="57aab-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="57aab-215">Gère un registre des identités qui stocke les identificateurs hello et les clés d’authentification de tous les périphériques hello autorisés tooconnect toohello portal.</span><span class="sxs-lookup"><span data-stu-id="57aab-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="57aab-216">Vous pouvez activer et désactiver des appareils via le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="57aab-217">Envoie des commandes tooyour périphériques pour le compte du portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="57aab-218">Appelle les méthodes sur vos appareils pour le compte du portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="57aab-219">Gère les représentations d’appareil pour tous les appareils inscrits.</span><span class="sxs-lookup"><span data-stu-id="57aab-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="57aab-220">Un double appareil stocke des valeurs de propriété de hello signalés par un périphérique.</span><span class="sxs-lookup"><span data-stu-id="57aab-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="57aab-221">Un double appareil stocke également les propriétés souhaitées, définies dans le portail solution hello pour hello appareil tooretrieve lors de la prochaine connexion.</span><span class="sxs-lookup"><span data-stu-id="57aab-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="57aab-222">Planifications de travaux tooset des propriétés pour plusieurs appareils ou d’appeler des méthodes sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="57aab-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="57aab-223">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="57aab-223">Azure Stream Analytics</span></span>

<span data-ttu-id="57aab-224">Dans la solution de surveillance à distance de hello [Analytique de flux de données Azure] [ lnk-asa] (ASA) distribue des messages de périphérique reçus par les composants hello IoT hub tooother principal pour le traitement ou de stockage.</span><span class="sxs-lookup"><span data-stu-id="57aab-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="57aab-225">Différentes tâches ASA réalisent des fonctions spécifiques, en fonction du contenu hello de messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="57aab-226">**Tâche 1 : Les informations de périphérique** filtre les messages d’informations de périphérique à partir de flux de messages entrants hello et les envoie de point de terminaison tooan concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="57aab-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="57aab-227">Un appareil envoie des messages d’informations de périphérique au démarrage et dans la réponse tooa **SendDeviceInfo** commande.</span><span class="sxs-lookup"><span data-stu-id="57aab-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="57aab-228">Cette tâche utilise hello suivant requête définition tooidentify **informations de périphérique** messages :</span><span class="sxs-lookup"><span data-stu-id="57aab-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="57aab-229">Ce travail envoie ses tooan sortie concentrateur d’événements pour un traitement ultérieur.</span><span class="sxs-lookup"><span data-stu-id="57aab-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="57aab-230">**tâche 2 : règles** compare les valeurs de télémétrie entrantes (température et humidité) aux seuils définis pour chaque appareil.</span><span class="sxs-lookup"><span data-stu-id="57aab-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="57aab-231">Les valeurs de seuil sont définies dans l’éditeur de règles hello disponible dans le portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="57aab-232">Chaque paire appareil/valeur est stockée par horodatage dans un objet blob que Stream Analytics lit comme des **Données de référence**.</span><span class="sxs-lookup"><span data-stu-id="57aab-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="57aab-233">travail de Hello compare une valeur non vide à seuil de jeu hello pour appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="57aab-234">Si elle dépasse hello ' >' de condition, produites par la tâche de hello un **alarme** événement qui indique que ce seuil hello est dépassé et fournit le dispositif de hello, valeur et les valeurs d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="57aab-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="57aab-235">Cette tâche utilise hello suivant requête définition tooidentify télémétrie les messages qui doivent déclencher une alarme :</span><span class="sxs-lookup"><span data-stu-id="57aab-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="57aab-236">Hello travail envoie ses tooan sortie concentrateur d’événements pour un traitement ultérieur et évite les détails de chaque alerte tooblob de stockage où portail de solution hello peut lire les informations d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="57aab-237">**Tâche 3 : Télémétrie** opère sur les flux de données de télémétrie de périphérique entrant hello de deux manières.</span><span class="sxs-lookup"><span data-stu-id="57aab-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="57aab-238">Hello envoie d’abord tous les messages de télémétrie à partir du stockage d’objets blob toopersistent hello périphériques de stockage à long terme.</span><span class="sxs-lookup"><span data-stu-id="57aab-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="57aab-239">Hello calcule ensuite humidité moyenne, minimale et maximale des valeurs sur une fenêtre glissante de cinq minutes et envoie ce stockage tooblob de données.</span><span class="sxs-lookup"><span data-stu-id="57aab-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="57aab-240">portail de solution Hello lit les données de télémétrie hello graphiques de hello de toopopulate de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="57aab-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="57aab-241">Cette tâche utilise hello après la définition de la requête :</span><span class="sxs-lookup"><span data-stu-id="57aab-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="57aab-242">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="57aab-242">Event Hubs</span></span>

<span data-ttu-id="57aab-243">Hello **Infos sur l’appareil** et **règles** les travaux ASA sortie leur données tooEvent concentrateurs tooreliably par progression sur toohello **processeur d’événements** en cours d’exécution Bonjour la tâche Web.</span><span class="sxs-lookup"><span data-stu-id="57aab-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="57aab-244">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="57aab-244">Azure storage</span></span>

<span data-ttu-id="57aab-245">solution de Hello utilise toopersist de stockage d’objets blob Azure toutes les données de télémétrie brut et résumée hello à partir d’appareils de hello dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="57aab-246">portail de Hello lit les données de télémétrie hello graphiques de hello de toopopulate de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="57aab-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="57aab-247">toodisplay alertes, portail de solution hello lit hello données de stockage d’objets blob qui enregistre lorsque hello a dépassé les valeurs de données de télémétrie configuré des valeurs de seuil.</span><span class="sxs-lookup"><span data-stu-id="57aab-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="57aab-248">solution de Hello utilise également des objets blob stockage toorecord hello seuil valeurs que vous définissez dans le portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="57aab-249">WebJobs</span><span class="sxs-lookup"><span data-stu-id="57aab-249">WebJobs</span></span>

<span data-ttu-id="57aab-250">En outre simulateurs de périphérique toohosting hello, hello WebJobs dans les solutions hello également hello d’hôte **processeur d’événements** en cours d’exécution dans une tâche Web Azure qui gère les réponses aux commandes.</span><span class="sxs-lookup"><span data-stu-id="57aab-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="57aab-251">Il utilise la commande réponse messages tooupdate hello commande historique de l’appareil (stocké dans la base de données de la base de données Cosmos hello).</span><span class="sxs-lookup"><span data-stu-id="57aab-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="57aab-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="57aab-252">Cosmos DB</span></span>

<span data-ttu-id="57aab-253">solution de Hello utilise une Cosmos DB de base de données toostore informations hello périphériques connectés toohello solution.</span><span class="sxs-lookup"><span data-stu-id="57aab-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="57aab-254">Ces informations comprennent l’historique de hello des commandes envoyées toodevices à partir du portail de solution hello et des méthodes appelées à partir du portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="57aab-255">Portail de la solution</span><span class="sxs-lookup"><span data-stu-id="57aab-255">Solution portal</span></span>

<span data-ttu-id="57aab-256">portail de solution Hello est une application web déployée dans le cadre de la solution de hello préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="57aab-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="57aab-257">pages de clés Hello dans le portail de solution hello sont hello le tableau de bord et de la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="57aab-258">tableau de bord</span><span class="sxs-lookup"><span data-stu-id="57aab-258">Dashboard</span></span>

<span data-ttu-id="57aab-259">Cette page dans l’application hello web utilise des contrôles javascript Power BI (consultez [référentiel de PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) données de télémétrie hello toovisualize à partir d’appareils de hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="57aab-260">solution de Hello utilise hello ASA télémétrie travail toowrite hello télémétrie tooblob stockage des données.</span><span class="sxs-lookup"><span data-stu-id="57aab-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="57aab-261">Liste des appareils</span><span class="sxs-lookup"><span data-stu-id="57aab-261">Device list</span></span>

<span data-ttu-id="57aab-262">Vous pouvez effectuer les opérations suivantes à partir de cette page dans le portail de solution hello :</span><span class="sxs-lookup"><span data-stu-id="57aab-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="57aab-263">Configurer un nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="57aab-263">Provision a new device.</span></span> <span data-ttu-id="57aab-264">Cette action définit l’id d’appareil unique hello et génère la clé d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="57aab-265">Il écrit les informations hello tooboth de périphérique hello Registre des identités IoT Hub et Cosmos DB base de données spécifique à la solution hello.</span><span class="sxs-lookup"><span data-stu-id="57aab-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="57aab-266">Gérer les propriétés de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="57aab-266">Manage device properties.</span></span> <span data-ttu-id="57aab-267">Cela comprend l’affichage des propriétés existantes et l’intégration des nouvelles propriétés.</span><span class="sxs-lookup"><span data-stu-id="57aab-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="57aab-268">Envoyer les commandes de périphérique tooa.</span><span class="sxs-lookup"><span data-stu-id="57aab-268">Send commands tooa device.</span></span>
* <span data-ttu-id="57aab-269">Afficher l’historique des commandes hello pour un périphérique.</span><span class="sxs-lookup"><span data-stu-id="57aab-269">View hello command history for a device.</span></span>
* <span data-ttu-id="57aab-270">Désactiver et activer les appareils.</span><span class="sxs-lookup"><span data-stu-id="57aab-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57aab-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57aab-271">Next steps</span></span>

<span data-ttu-id="57aab-272">Hello billets de blog TechNet suivants fournissent plus de détails sur hello solution préconfigurée de surveillance à distance :</span><span class="sxs-lookup"><span data-stu-id="57aab-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="57aab-273">La surveillance à distance IoT Suite - sous le capot de hello-</span><span class="sxs-lookup"><span data-stu-id="57aab-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="57aab-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (en anglais)</span><span class="sxs-lookup"><span data-stu-id="57aab-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="57aab-275">Vous pouvez continuer la mise en route avec IoT Suite en lisant hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="57aab-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="57aab-276">[Se connecter à votre solution préconfigurée de surveillance à distance de toohello périphérique][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="57aab-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="57aab-277">[Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="57aab-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
