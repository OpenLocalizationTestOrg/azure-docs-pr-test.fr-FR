---
title: "propriétés de double de l’appareil Azure IoT Hub aaaUse (nœud) | Documents Microsoft"
description: "Comment jumeaux dispositif de Azure IoT Hub toouse tooconfigure périphériques. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé et une application de service qui modifie une configuration de l’appareil à l’aide d’un double de l’appareil."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="f162f-104">Périphériques de tooconfigure propriétés utilisation souhaitée (nœud)</span><span class="sxs-lookup"><span data-stu-id="f162f-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="f162f-105">À la fin de hello de ce didacticiel, vous aurez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="f162f-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="f162f-106">**SimulateDeviceConfiguration.js**, une application d’appareil simulé qui attend une mise à jour de la configuration souhaitée et signale l’état hello d’un processus de mise à jour de configuration simulé.</span><span class="sxs-lookup"><span data-stu-id="f162f-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="f162f-107">**SetDesiredConfigurationAndQuery.js**, une application back-end Node.js, qui définit hello souhaitée de configuration sur un appareil et requêtes hello le processus de mise à jour de configuration.</span><span class="sxs-lookup"><span data-stu-id="f162f-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="f162f-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.</span><span class="sxs-lookup"><span data-stu-id="f162f-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="f162f-109">toocomplete ce didacticiel, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="f162f-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="f162f-110">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f162f-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f162f-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="f162f-111">An active Azure account.</span></span> <span data-ttu-id="f162f-112">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="f162f-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="f162f-113">Si vous avez suivi hello [prise en main jumeaux de périphérique] [ lnk-twin-tutorial] didacticiel, vous disposez déjà d’un IoT hub et une identité d’appareil appelé **myDeviceId**; et vous pouvez ignorer toohello [ Créer l’application d’appareil simulé hello] [ lnk-how-to-configure-createapp] section.</span><span class="sxs-lookup"><span data-stu-id="f162f-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="f162f-114">Créer l’application d’appareil simulé hello</span><span class="sxs-lookup"><span data-stu-id="f162f-114">Create hello simulated device app</span></span>
<span data-ttu-id="f162f-115">Dans cette section, vous créez une application de console Node.js qui connecte le concentrateur tooyour **myDeviceId**et attend une mise à jour de la configuration souhaitée et signale ensuite les mises à jour sur le processus de mise à jour de configuration hello simulé.</span><span class="sxs-lookup"><span data-stu-id="f162f-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="f162f-116">Créez un dossier vide nommé **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="f162f-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="f162f-117">Bonjour **simulatedeviceconfiguration** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="f162f-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f162f-118">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="f162f-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f162f-119">Votre invite de commandes Bonjour **simulatedeviceconfiguration** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil**, et **azure-iot-périphérique-mqtt**package :</span><span class="sxs-lookup"><span data-stu-id="f162f-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="f162f-120">À l’aide d’un éditeur de texte, créez un nouveau **SimulateDeviceConfiguration.js** fichier Bonjour **simulatedeviceconfiguration** dossier.</span><span class="sxs-lookup"><span data-stu-id="f162f-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="f162f-121">Ajouter hello suivant code toohello **SimulateDeviceConfiguration.js** de fichiers et remplacez-le par hello **{chaîne de connexion de périphérique}** espace réservé avec la chaîne de connexion de périphérique hello vous avez copié quand vous créé hello **myDeviceId** identité d’appareil :</span><span class="sxs-lookup"><span data-stu-id="f162f-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="f162f-122">Hello **Client** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="f162f-123">Hello le code précédent, une fois qu’il initialise hello **Client** de l’objet, récupère hello double de périphérique pour **myDeviceId**et l’attache un gestionnaire de mise à jour hello sur les propriétés de votre choisies.</span><span class="sxs-lookup"><span data-stu-id="f162f-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="f162f-124">Gestionnaire de Hello vérifie qu’une demande de modification de configuration en comparant hello configIds, puis appelle une méthode qui démarre la modification de la configuration hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="f162f-125">Notez que pour des raisons de hello de simplicité, de code hello précédent utilise une valeur par défaut codées en dur pour la configuration initiale hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="f162f-126">Une application réelle chargerait probablement la configuration à partir d’un stockage local.</span><span class="sxs-lookup"><span data-stu-id="f162f-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f162f-127">Événements de modification de propriété souhaitée sont toujours émis une seule fois lors de la connexion du périphérique, assurez-vous que toocheck qu’il existe une modification réelle dans hello souhaité propriétés avant d’effectuer une action.</span><span class="sxs-lookup"><span data-stu-id="f162f-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="f162f-128">Ajouter hello suivant les méthodes avant hello `client.open()` invocation :</span><span class="sxs-lookup"><span data-stu-id="f162f-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="f162f-129">Hello **initConfigChange** mises à jour de la méthode a signalé des propriétés sur l’objet de double hello périphérique local avec la demande de mise à jour de configuration hello et jeux hello état trop**en attente**, puis les mises à jour hello appareil double sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="f162f-130">Après la mise à jour de double de périphérique hello, elle simule un processus à long terme qui arrête l’exécution de hello de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="f162f-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="f162f-131">Cette double de périphérique local hello méthode mises à jour de l’a signalé des propriétés définissant le statut de hello trop**réussite** et suppression hello **pendingConfig** objet.</span><span class="sxs-lookup"><span data-stu-id="f162f-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="f162f-132">Il met ensuite à jour le double de périphérique hello sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="f162f-133">À noter que, la bande passante toosave indiqué propriétés sont mises à jour en spécifiant uniquement les toobe hello propriétés modifiées (nommé **correctif** Bonjour au-dessus de code), au lieu de remplacer l’ensemble du document hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f162f-134">Ce didacticiel ne simule pas de comportement pour des mises à jour de configuration simultanées.</span><span class="sxs-lookup"><span data-stu-id="f162f-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="f162f-135">Certains processus de mise à jour de configuration peuvent être en mesure de tooaccommodate des modifications de configuration de la cible pendant l’exécution de mise à jour hello, d’autres peuvent comporter des tooqueue, ainsi que d’autres utilisateurs peuvent rejeter les avec une condition d’erreur.</span><span class="sxs-lookup"><span data-stu-id="f162f-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="f162f-136">Assurez-vous que tooconsider hello le comportement souhaité pour votre processus de configuration spécifique et ajouter une logique approprié de hello avant le lancement de la modification de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="f162f-137">Exécutez l’application hello :</span><span class="sxs-lookup"><span data-stu-id="f162f-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="f162f-138">Vous devez voir le message de type hello `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="f162f-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="f162f-139">Gardez à l’application hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f162f-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="f162f-140">Créer l’application de service hello</span><span class="sxs-lookup"><span data-stu-id="f162f-140">Create hello service app</span></span>
<span data-ttu-id="f162f-141">Dans cette section, vous allez créer une application de console Node.js que hello mises à jour *propriétés souhaitée* sur hello double de périphérique associé **myDeviceId** avec un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f162f-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="f162f-142">Il interroge jumeaux de périphérique hello stockées dans le hub IoT de hello et montre la différence hello entre hello souhaitée et a signalé des configurations de périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="f162f-143">Créez un dossier vide nommé **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="f162f-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="f162f-144">Bonjour **setdesiredandqueryapp** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="f162f-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f162f-145">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="f162f-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f162f-146">Votre invite de commandes Bonjour **setdesiredandqueryapp** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :</span><span class="sxs-lookup"><span data-stu-id="f162f-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="f162f-147">À l’aide d’un éditeur de texte, créez un nouveau **SetDesiredAndQuery.js** fichier Bonjour **addtagsandqueryapp** dossier.</span><span class="sxs-lookup"><span data-stu-id="f162f-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="f162f-148">Ajouter hello suivant code toohello **SetDesiredAndQuery.js** de fichiers et remplacez-le par hello **{chaîne de connexion de hub iot}** espace réservé par chaîne de connexion de IoT Hub vous avez copié lorsque vous avez créé votre hub de hello :</span><span class="sxs-lookup"><span data-stu-id="f162f-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="f162f-149">Hello **Registre** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="f162f-150">Hello le code précédent, une fois qu’il initialise hello **Registre** de l’objet, récupère hello double de périphérique pour **myDeviceId**et met à jour ses propriétés souhaitées par un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f162f-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="f162f-151">Après cela, il appelle hello **queryTwins** fonction événement 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="f162f-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f162f-152">Cette application interroge IoT Hub toutes les 10 secondes à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="f162f-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="f162f-153">Utilisez des requêtes toogenerate orientés utilisateur rapports entre plusieurs appareils et pas les modifications toodetect.</span><span class="sxs-lookup"><span data-stu-id="f162f-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="f162f-154">Si votre solution nécessite des notifications d’événements d’appareil en temps réel, utilisez des [notifications jumelles][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="f162f-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="f162f-155">.</span><span class="sxs-lookup"><span data-stu-id="f162f-155">.</span></span>

1. <span data-ttu-id="f162f-156">Ajouter hello suivant code juste avant hello `registry.getDeviceTwin()` hello de tooimplement invocation **queryTwins** (fonction) :</span><span class="sxs-lookup"><span data-stu-id="f162f-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="f162f-157">requêtes de code précédentes Hello hello jumeaux appareil stockées dans le hub IoT de hello et commander des photos hello souhaitée et a signalé des configurations de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f162f-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="f162f-158">Consultez toohello [langage de requête IoT Hub] [ lnk-query] toolearn comment toogenerate enrichi les rapports sur tous vos appareils.</span><span class="sxs-lookup"><span data-stu-id="f162f-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="f162f-159">Avec **SimulateDeviceConfiguration.js** en cours d’exécution, exécutez l’application hello avec :</span><span class="sxs-lookup"><span data-stu-id="f162f-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="f162f-160">Vous devez voir configuration signalé de hello modifier à partir de **réussite** trop**en attente** trop**réussite** à nouveau avec active de nouveau hello fréquence d’envoi des cinq minutes au lieu de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f162f-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f162f-161">Il existe un délai d’une minute tooa entre l’opération de rapport d’appareil hello et le résultat de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="f162f-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="f162f-162">Il s’agit de tooenable hello requête infrastructure toowork à très grande échelle.</span><span class="sxs-lookup"><span data-stu-id="f162f-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="f162f-163">tooretrieve des vues cohérentes d’un double d’appareil unique utilisent hello **getDeviceTwin** méthode Bonjour **Registre** classe.</span><span class="sxs-lookup"><span data-stu-id="f162f-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="f162f-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f162f-164">Next steps</span></span>
<span data-ttu-id="f162f-165">Dans ce didacticiel, vous définissez la configuration souhaitée en tant que *propriétés souhaitée* à partir d’une application back-end et écrit un toodetect d’application appareil simulé qui changent et simuler un processus de mise à jour de plusieurs étapes reporting son état en tant que  *signalé propriétés* double de périphérique toohello.</span><span class="sxs-lookup"><span data-stu-id="f162f-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="f162f-166">Hello utilisation suivant comment les ressources toolearn à :</span><span class="sxs-lookup"><span data-stu-id="f162f-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="f162f-167">envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),</span><span class="sxs-lookup"><span data-stu-id="f162f-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="f162f-168">planifier ou exécuter des opérations sur les grands ensembles de périphériques Voir hello [planification et les tâches de diffusion] [ lnk-schedule-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f162f-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="f162f-169">contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur), avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f162f-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
