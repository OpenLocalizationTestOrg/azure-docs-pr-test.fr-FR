---
title: "Utilisation des propriétés des représentations physiques Azure IoT Hub (Node) | Microsoft Docs"
description: "Guide d’utilisation des représentations d’appareils Azure IoT Hub pour configurer des appareils. Les kits de développement logiciel (SDK) Azure IoT pour Node.js permettent d’implémenter une application d’appareil simulé et une application de service qui modifie la configuration d’un appareil à l’aide d’une représentation d’appareil."
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
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="4d539-104">Utilisation des propriétés souhaitées pour configurer des appareils (Node)</span><span class="sxs-lookup"><span data-stu-id="4d539-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="4d539-105">À la fin de ce didacticiel, vous disposerez de deux applications console Node.js :</span><span class="sxs-lookup"><span data-stu-id="4d539-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="4d539-106">**SimulateDeviceConfiguration.js**, application d’appareil simulée qui attend une mise à jour de configuration souhaitée, et signale l’état d’un processus de mise à jour de configuration simulée.</span><span class="sxs-lookup"><span data-stu-id="4d539-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="4d539-107">**SetDesiredConfigurationAndQuery.js**, application Node.js sur le serveur principal qui définit la configuration souhaitée sur un appareil, et interroge le processus de mise à jour de configuration.</span><span class="sxs-lookup"><span data-stu-id="4d539-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="4d539-108">L’article [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks] fournit des informations sur les Kits de développement logiciel (SDK) IoT que vous pouvez utiliser pour générer des applications pour appareil et des applications principales.</span><span class="sxs-lookup"><span data-stu-id="4d539-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="4d539-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4d539-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="4d539-110">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4d539-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="4d539-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4d539-111">An active Azure account.</span></span> <span data-ttu-id="4d539-112">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="4d539-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="4d539-113">Si vous avez suivi le didacticiel [Prise en main des représentations d’appareil][lnk-twin-tutorial], vous avez déjà un IoT Hub et une identité d’appareil nommée **myDeviceId**. Vous pouvez passer à la section [Créer l’application pour appareil simulée][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="4d539-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="4d539-114">Créer l’application d’appareil simulée</span><span class="sxs-lookup"><span data-stu-id="4d539-114">Create the simulated device app</span></span>
<span data-ttu-id="4d539-115">Dans cette section, vous créez une application console Node.js qui se connecte à votre hub en tant que **myDeviceId**, attend une mise à jour de la configuration souhaitée, puis signale des mises à jour sur le processus de mise à jour de configuration simulée.</span><span class="sxs-lookup"><span data-stu-id="4d539-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="4d539-116">Créez un dossier vide nommé **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="4d539-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="4d539-117">Dans le dossier **simulatedeviceconfiguration**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="4d539-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="4d539-118">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="4d539-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4d539-119">À l’invite de commandes, dans le dossier **simulatedeviceconfiguration**, exécutez la commande suivante pour installer les packages **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="4d539-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="4d539-120">À l’aide d’un éditeur de texte, créez un fichier **SimulateDeviceConfiguration.js** dans le dossier **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="4d539-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="4d539-121">Ajoutez le code suivant au fichier **SimulateDeviceConfiguration.js**, puis remplacez l’espace réservé **{device connection string}** par la chaîne de connexion à l’appareil que vous avez copiée lors de la création de l’identité d’appareil **myDeviceId** :</span><span class="sxs-lookup"><span data-stu-id="4d539-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="4d539-122">L’objet **Client** expose toutes les méthodes requises pour interagir avec des représentations d’appareil à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4d539-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="4d539-123">Le code précédent, après avoir initialisé l’objet **Client**, récupère la représentation d’appareil de **myDeviceId**, puis attache un gestionnaire pour la mise à jour sur les propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="4d539-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="4d539-124">Le gestionnaire vérifie l’existence d’une demande de modification de configuration réelle en comparant les configIds, puis appelle une méthode qui démarre la modification de configuration.</span><span class="sxs-lookup"><span data-stu-id="4d539-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="4d539-125">Notez que, par souci de simplicité, le code précédent utilise une valeur par défaut codées en dur pour la configuration initiale.</span><span class="sxs-lookup"><span data-stu-id="4d539-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="4d539-126">Une application réelle chargerait probablement la configuration à partir d’un stockage local.</span><span class="sxs-lookup"><span data-stu-id="4d539-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4d539-127">Les événements de modification de propriété souhaitée étant toujours émis une seule fois lors de la connexion de l’appareil, assurez-vous de l’existence d’une modification réelle dans les propriétés souhaitées avant d’exécuter toute action.</span><span class="sxs-lookup"><span data-stu-id="4d539-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="4d539-128">Avant d’appeler `client.open()`ajoutez les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d539-128">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="4d539-129">La méthode **initConfigChange** met à jour les propriétés signalées sur l’objet de représentation d’appareil local avec la demande de mise à jour de configuration, et définit l’état sur **Pending** (En attente), puis met à jour la représentation d’appareil sur le service.</span><span class="sxs-lookup"><span data-stu-id="4d539-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="4d539-130">Après la mise à jour de la représentation d’appareil, elle simule un processus de longue durée qui s’achève par l’exécution de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="4d539-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="4d539-131">Cette méthode met à jour les propriétés signalées de la représentation d’appareil locale en définissant l’état sur **Success** (Réussite) et en supprimant l’objet **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="4d539-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="4d539-132">Ensuite, elle met à jour la représentation d’appareil sur le service.</span><span class="sxs-lookup"><span data-stu-id="4d539-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="4d539-133">Notez que, pour économiser la bande passante, les propriétés signalées sont mises à jour en spécifiant uniquement les propriétés à modifier (nommées **patch** dans le code ci-dessus), au lieu de remplacer le document entier.</span><span class="sxs-lookup"><span data-stu-id="4d539-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4d539-134">Ce didacticiel ne simule pas de comportement pour des mises à jour de configuration simultanées.</span><span class="sxs-lookup"><span data-stu-id="4d539-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="4d539-135">Certains processus de mise à jour de configuration peuvent s’adapter à des modifications de configuration de la cible en cours de mise à jour, d’autres peuvent avoir à les mettre en file d’attente, et d’autres encore peuvent les refuser avec une condition d’erreur.</span><span class="sxs-lookup"><span data-stu-id="4d539-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="4d539-136">Prenez en considération le comportement souhaité pour votre processus de configuration spécifique, et ajoutez la logique appropriée avant de lancer la modification de la configuration.</span><span class="sxs-lookup"><span data-stu-id="4d539-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="4d539-137">Exécutez l’application d’appareil :</span><span class="sxs-lookup"><span data-stu-id="4d539-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="4d539-138">Vous devriez voir le message `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="4d539-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="4d539-139">Gardez l’application active.</span><span class="sxs-lookup"><span data-stu-id="4d539-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="4d539-140">Créer l’application de service</span><span class="sxs-lookup"><span data-stu-id="4d539-140">Create the service app</span></span>
<span data-ttu-id="4d539-141">Dans cette section, vous allez créer une application console Node.js qui met à jour les *propriétés souhaitées* sur la représentation d’appareil associée à **myDeviceId** avec un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="4d539-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="4d539-142">Elle interroge ensuite les représentations d’appareil stockées dans l’IoT Hub, puis affiche la différence entre les configurations souhaitées et signalées de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4d539-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="4d539-143">Créez un dossier vide nommé **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="4d539-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="4d539-144">Dans le dossier **setdesiredandqueryapp**, créez un fichier package.json à l’aide de la commande ci-dessous à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="4d539-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="4d539-145">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="4d539-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4d539-146">À l’invite de commandes, dans le dossier **setdesiredandqueryapp**, exécutez la commande suivante pour installer le package **azure-iothub** :</span><span class="sxs-lookup"><span data-stu-id="4d539-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="4d539-147">À l’aide d’un éditeur de texte, créez un fichier **SetDesiredAndQuery.js** dans le dossier **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="4d539-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="4d539-148">Ajoutez le code suivant au fichier **SetDesiredAndQuery.js**, puis remplacez l’espace réservé **{iot hub connection string}** par la chaîne de connexion que vous avez copiée lors de la création de votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="4d539-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="4d539-149">L’objet **Registry** expose toutes les méthodes requises pour interagir avec des représentations d’appareil à partir du service.</span><span class="sxs-lookup"><span data-stu-id="4d539-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="4d539-150">Le code précédent, après avoir initialisé l’objet **Registry**, récupère la représentation d’appareil de **myDeviceId**, puis met à jour ses propriétés souhaitées avec un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="4d539-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="4d539-151">Ensuite, il appelle l’événement de fonction **queryTwins** pendant 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="4d539-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4d539-152">Cette application interroge IoT Hub toutes les 10 secondes à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="4d539-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="4d539-153">Utilisez des requêtes pour générer des rapports côté utilisateur sur plusieurs appareils, non pour détecter des modifications.</span><span class="sxs-lookup"><span data-stu-id="4d539-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="4d539-154">Si votre solution nécessite des notifications d’événements d’appareil en temps réel, utilisez des [notifications jumelles][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="4d539-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="4d539-155">.</span><span class="sxs-lookup"><span data-stu-id="4d539-155">.</span></span>

1. <span data-ttu-id="4d539-156">Ajoutez le code suivant juste devant l’appel de `registry.getDeviceTwin()` pour implémenter la fonction **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="4d539-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
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
   
    <span data-ttu-id="4d539-157">Le code précédent interroge les représentations d’appareil stockées dans l’IoT Hub, et imprime les configurations de télémétrie souhaitées et signalées.</span><span class="sxs-lookup"><span data-stu-id="4d539-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="4d539-158">Pour savoir comment générer des rapports riches sur tous vos appareils, consultez le [langage de requête IoT Hub][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="4d539-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="4d539-159">Avec **SimulateDeviceConfiguration.js** en cours d’exécution, exécutez l’application avec :</span><span class="sxs-lookup"><span data-stu-id="4d539-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="4d539-160">Vous devriez voir la configuration signalée passer de **Success** (Réussite) à **Pending** (En attente), puis de nouveau à **Success** (Réussite), avec la nouvelle fréquence d’envoi active de cinq minutes au lieu de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="4d539-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4d539-161">Un délai pouvant atteindre une minute s’écoule entre l’opération de signalement de l’appareil et le résultat de la requête.</span><span class="sxs-lookup"><span data-stu-id="4d539-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="4d539-162">Il permet à l’infrastructure de requête d’opérer à très grande échelle.</span><span class="sxs-lookup"><span data-stu-id="4d539-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="4d539-163">Pour récupérer des vues cohérentes d’une représentation d’appareil, utilisez la méthode **getDeviceTwin** dans la classe **Registry**.</span><span class="sxs-lookup"><span data-stu-id="4d539-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="4d539-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d539-164">Next steps</span></span>
<span data-ttu-id="4d539-165">Dans ce didacticiel, vous avez défini une configuration souhaitée en tant que *propriétés souhaitées* à partir d’une application principale, et écrit une application pour appareil simulée afin de détecter cette modification et de simuler un processus de mise à jour en plusieurs étapes signalant son état en tant que *propriétés signalées* à la représentation d’appareil.</span><span class="sxs-lookup"><span data-stu-id="4d539-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="4d539-166">Utilisez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d539-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="4d539-167">Pour savoir comment envoyer les données de télémétrie à partir d’appareils, consultez le didacticiel [Prise en main d’IoT Hub][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="4d539-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="4d539-168">Pour savoir comment planifier ou exécuter des opérations sur de grands ensembles d’appareils, consultez le didacticiel [Planifier et diffuser des travaux][lnk-schedule-jobs].</span><span class="sxs-lookup"><span data-stu-id="4d539-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="4d539-169">Pour savoir comment contrôler des appareils de façon interactive (par exemple en mettant en marche un ventilateur à partir d’une application contrôlée par l’utilisateur), consultez le didacticiel [Utiliser des méthodes directes][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="4d539-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
