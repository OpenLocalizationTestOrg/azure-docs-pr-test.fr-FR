---
title: "Utilisation des propriétés des représentations physiques Azure IoT Hub (.NET/Node) | Microsoft Docs"
description: "Guide d’utilisation des représentations d’appareils Azure IoT Hub pour configurer des appareils. Vous utilisez Azure IoT device SDK pour Node.js afin d’implémenter une application d’appareil simulé et Azure IoT service SDK pour .NET afin d’implémenter une application de service qui modifie une configuration d’appareil avec une représentation d’appareil."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 78b4523fa7d0c056f84214429730a5df1bcdcef7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="110dd-104">Utilisation des propriétés souhaitées pour configurer des appareils</span><span class="sxs-lookup"><span data-stu-id="110dd-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="110dd-105">À la fin de ce didacticiel, vous disposerez de deux applications console :</span><span class="sxs-lookup"><span data-stu-id="110dd-105">At the end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="110dd-106">**SimulateDeviceConfiguration.js**, application d’appareil simulée qui attend une mise à jour de configuration souhaitée, et signale l’état d’un processus de mise à jour de configuration simulée.</span><span class="sxs-lookup"><span data-stu-id="110dd-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="110dd-107">**SetDesiredConfigurationAndQuery**, application .NET sur le serveur principal qui définit la configuration souhaitée sur un appareil, et interroge le processus de mise à jour de configuration.</span><span class="sxs-lookup"><span data-stu-id="110dd-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="110dd-108">L’article [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks] fournit des informations sur les Kits de développement logiciel (SDK) IoT que vous pouvez utiliser pour générer des applications pour appareil et des applications principales.</span><span class="sxs-lookup"><span data-stu-id="110dd-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="110dd-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="110dd-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="110dd-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="110dd-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="110dd-111">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="110dd-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="110dd-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="110dd-112">An active Azure account.</span></span> <span data-ttu-id="110dd-113">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="110dd-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="110dd-114">Si vous avez suivi le didacticiel [Prise en main des jumeaux d’appareils][lnk-twin-tutorial], vous avez déjà un IoT Hub et une identité d’appareil nommée **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="110dd-114">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="110dd-115">Vous pouvez donc passer à la section [Créer l’application d’appareil simulé][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="110dd-115">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="110dd-116">Créer l’application d’appareil simulée</span><span class="sxs-lookup"><span data-stu-id="110dd-116">Create the simulated device app</span></span>
<span data-ttu-id="110dd-117">Dans cette section, vous créez une application console Node.js qui se connecte à votre hub en tant que **myDeviceId**, attend une mise à jour de la configuration souhaitée, puis signale des mises à jour sur le processus de mise à jour de configuration simulée.</span><span class="sxs-lookup"><span data-stu-id="110dd-117">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="110dd-118">Créez un dossier vide nommé **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="110dd-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="110dd-119">Dans le dossier **simulatedeviceconfiguration**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="110dd-119">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="110dd-120">Acceptez toutes les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="110dd-120">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="110dd-121">À l’invite de commandes, dans le dossier **simulatedeviceconfiguration**, exécutez la commande suivante pour installer les packages **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="110dd-121">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="110dd-122">À l’aide d’un éditeur de texte, créez un fichier **SimulateDeviceConfiguration.js** dans le dossier **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="110dd-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="110dd-123">Ajoutez le code suivant au fichier **SimulateDeviceConfiguration.js**, puis remplacez l’espace réservé **{device connection string}** par la chaîne de connexion à l’appareil que vous avez copiée lors de la création de l’identité d’appareil **myDeviceId** :</span><span class="sxs-lookup"><span data-stu-id="110dd-123">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="110dd-124">L’objet **Client** expose toutes les méthodes requises pour interagir avec des représentations d’appareil à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="110dd-124">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="110dd-125">Ce code initialise l’objet **Client**, récupère le jumeau d’appareil de **myDeviceId**, puis attache un gestionnaire pour la mise à jour sur les *propriétés souhaitées*.</span><span class="sxs-lookup"><span data-stu-id="110dd-125">This code initializes the **Client** object, retrieves the device twin for **myDeviceId**, and then attaches a handler for the update on *desired properties*.</span></span> <span data-ttu-id="110dd-126">Le gestionnaire vérifie l’existence d’une demande de modification de configuration réelle en comparant les configIds, puis appelle une méthode qui démarre la modification de configuration.</span><span class="sxs-lookup"><span data-stu-id="110dd-126">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="110dd-127">Notez que, par souci de simplicité, ce code utilise une valeur par défaut codée en dur pour la configuration initiale.</span><span class="sxs-lookup"><span data-stu-id="110dd-127">Note that for the sake of simplicity, this code uses a hard-coded default for the initial configuration.</span></span> <span data-ttu-id="110dd-128">Une application réelle chargerait probablement la configuration à partir d’un stockage local.</span><span class="sxs-lookup"><span data-stu-id="110dd-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="110dd-129">Les événements de modification de propriété souhaités sont toujours émis une seule fois lors de la connexion de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="110dd-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="110dd-130">Pensez à vérifier que les propriétés souhaitées ont bien été modifiées avant d’exécuter une action.</span><span class="sxs-lookup"><span data-stu-id="110dd-130">Make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="110dd-131">Avant d’appeler `client.open()`ajoutez les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="110dd-131">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="110dd-132">La méthode **initConfigChange** met à jour les propriétés signalées sur l’objet de représentation d’appareils local avec la demande de mise à jour de configuration, et définit l’état sur **Pending** (En attente), puis met à jour la représentation d’appareils sur le service.</span><span class="sxs-lookup"><span data-stu-id="110dd-132">The **initConfigChange** method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="110dd-133">Après la mise à jour de la représentation d’appareil, elle simule un processus de longue durée qui s’achève par l’exécution de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="110dd-133">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="110dd-134">Cette méthode met à jour les propriétés signalées locales en définissant l’état sur **Success** (Réussite) et en supprimant l’objet **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="110dd-134">This method updates the local reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="110dd-135">Ensuite, elle met à jour la représentation d’appareils sur le service.</span><span class="sxs-lookup"><span data-stu-id="110dd-135">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="110dd-136">Notez que, pour économiser la bande passante, les propriétés signalées sont mises à jour en spécifiant uniquement les propriétés à modifier (nommées **patch** dans le code ci-dessus), au lieu de remplacer le document entier.</span><span class="sxs-lookup"><span data-stu-id="110dd-136">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="110dd-137">Ce didacticiel ne simule pas de comportement pour des mises à jour de configuration simultanées.</span><span class="sxs-lookup"><span data-stu-id="110dd-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="110dd-138">Certains processus de mise à jour de configuration peuvent s’adapter à des modifications de configuration de la cible en cours de mise à jour, d’autres peuvent avoir à les mettre en file d’attente, et d’autres encore peuvent les refuser avec une condition d’erreur.</span><span class="sxs-lookup"><span data-stu-id="110dd-138">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="110dd-139">Prenez en considération le comportement souhaité pour votre processus de configuration spécifique, et ajoutez la logique appropriée avant de lancer la modification de la configuration.</span><span class="sxs-lookup"><span data-stu-id="110dd-139">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="110dd-140">Exécutez l’application d’appareil :</span><span class="sxs-lookup"><span data-stu-id="110dd-140">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="110dd-141">Vous devriez voir le message `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="110dd-141">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="110dd-142">Gardez l’application active.</span><span class="sxs-lookup"><span data-stu-id="110dd-142">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="110dd-143">Créer l’application de service</span><span class="sxs-lookup"><span data-stu-id="110dd-143">Create the service app</span></span>
<span data-ttu-id="110dd-144">Dans cette section, vous créez une application console .NET qui met à jour les *propriétés souhaitées* sur la représentation d’appareils associée à **myDeviceId** avec un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="110dd-144">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="110dd-145">Elle interroge ensuite les représentations d’appareils stockées dans l’IoT Hub, puis affiche la différence entre les configurations souhaitées et signalées de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="110dd-145">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="110dd-146">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application Console** .</span><span class="sxs-lookup"><span data-stu-id="110dd-146">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="110dd-147">Nommez le projet **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="110dd-147">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. <span data-ttu-id="110dd-149">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **SetDesiredConfigurationAndQuery**, puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="110dd-149">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="110dd-150">Dans la fenêtre **Gestionnaire de package NuGet**, cliquez sur **Parcourir**, puis recherchez **microsoft.azure.devices**. Cliquez ensuite sur **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="110dd-150">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="110dd-151">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="110dd-151">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="110dd-153">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="110dd-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="110dd-154">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="110dd-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="110dd-155">Remplacez la valeur d’espace réservé par la chaîne de connexion IoT Hub pour le hub créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="110dd-155">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="110dd-156">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="110dd-156">Add the following method to the **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="110dd-157">L’objet **Registry** expose toutes les méthodes requises pour interagir avec des représentations d’appareil à partir du service.</span><span class="sxs-lookup"><span data-stu-id="110dd-157">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="110dd-158">Ce code initialise l’objet **Registry**, récupère le jumeau d’appareils de **myDeviceId**, puis met à jour ses propriétés souhaitées avec un nouvel objet de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="110dd-158">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="110dd-159">Après cela, il interroge toutes les 10 secondes les jumeaux d’appareils stockées dans l’IoT Hub, puis imprime les configurations de télémétrie souhaitées et signalées.</span><span class="sxs-lookup"><span data-stu-id="110dd-159">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="110dd-160">Pour savoir comment générer des rapports riches sur tous vos appareils, voir le [langage de requête IoT Hub][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="110dd-160">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="110dd-161">Cette application interroge IoT Hub toutes les 10 secondes à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="110dd-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="110dd-162">Utilisez des requêtes pour générer des rapports côté utilisateur sur plusieurs appareils, non pour détecter des modifications.</span><span class="sxs-lookup"><span data-stu-id="110dd-162">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="110dd-163">Si votre solution nécessite des notifications d’événements d’appareil en temps réel, utilisez des [notifications jumelles][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="110dd-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="110dd-164">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="110dd-164">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="110dd-165">Dans l’Explorateur de solutions, sélectionnez **Définir les projets de démarrage...** et vérifiez que l’**Action** définie pour le projet **SetDesiredConfigurationAndQuery** est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="110dd-165">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="110dd-166">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="110dd-166">Build the solution.</span></span>
1. <span data-ttu-id="110dd-167">Avec **SimulateDeviceConfiguration.js** en cours d’exécution, exécutez l’application .NET depuis Visual Studio avec **F5** et vous devriez voir la configuration signalée passer de **Success** (Réussite) à **Pending** (En attente), puis de nouveau à **Success** (Réussite), avec la nouvelle fréquence d’envoi active de cinq minutes au lieu de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="110dd-167">With **SimulateDeviceConfiguration.js** running, run the .NET application from Visual Studio using **F5** and you should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Appareil configuré correctement][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="110dd-169">Un délai pouvant atteindre une minute s’écoule entre l’opération de signalement de l’appareil et le résultat de la requête.</span><span class="sxs-lookup"><span data-stu-id="110dd-169">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="110dd-170">Il permet à l’infrastructure de requête d’opérer à très grande échelle.</span><span class="sxs-lookup"><span data-stu-id="110dd-170">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="110dd-171">Pour récupérer des vues cohérentes d’une représentation d’appareil, utilisez la méthode **getDeviceTwin** dans la classe **Registry**.</span><span class="sxs-lookup"><span data-stu-id="110dd-171">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="110dd-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="110dd-172">Next steps</span></span>
<span data-ttu-id="110dd-173">Dans ce didacticiel, vous avez défini une configuration souhaitée en tant que *propriétés souhaitées* à partir du serveur principal et écrit une application d’appareil pour détecter cette modification et simuler un processus de mise à jour en plusieurs étapes signalant son état par le biais des propriétés signalées.</span><span class="sxs-lookup"><span data-stu-id="110dd-173">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="110dd-174">Utilisez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="110dd-174">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="110dd-175">Pour savoir comment envoyer les données de télémétrie à partir d’appareils, consultez le didacticiel [Prise en main d’IoT Hub][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="110dd-175">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="110dd-176">Pour savoir comment planifier ou exécuter des opérations sur de grands ensembles d’appareils, consultez le didacticiel [Planifier et diffuser des travaux][lnk-schedule-jobs].</span><span class="sxs-lookup"><span data-stu-id="110dd-176">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="110dd-177">Pour savoir comment contrôler des appareils de façon interactive (par exemple en mettant en marche un ventilateur à partir d’une application contrôlée par l’utilisateur), consultez le didacticiel [Utiliser des méthodes directes][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="110dd-177">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
