---
title: "aaaConnect un appareil à l’aide de Node.js | Documents Microsoft"
description: "Décrit comment tooconnect un toohello appareil Azure IoT Suite préconfiguré solution d’analyse à distance à l’aide d’une application écrite en Node.js."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="bc2aa-103">Se connecter à votre solution préconfigurée (Node.js) de surveillance à distance de toohello périphérique</span><span class="sxs-lookup"><span data-stu-id="bc2aa-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="bc2aa-104">Création d’un exemple de solution Node.js</span><span class="sxs-lookup"><span data-stu-id="bc2aa-104">Create a node.js sample solution</span></span>

<span data-ttu-id="bc2aa-105">Vérifiez que Node.js version 0.11.5 ou ultérieure est installé sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="bc2aa-106">Vous pouvez exécuter `node --version` à la version de hello toocheck hello ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="bc2aa-107">Créez un dossier nommé **RemoteMonitoring** sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="bc2aa-108">Parcourir le dossier toothis dans votre environnement de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="bc2aa-109">Hello exécution suivant des commandes toodownload et installer des packages hello vous devez toocomplete hello exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="bc2aa-110">Bonjour **RemoteMonitoring** dossier, créez un fichier appelé **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="bc2aa-111">Ouvrez ce fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="bc2aa-112">Bonjour **remote_monitoring.js** , ajoutez les éléments suivants de hello `require` instructions :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="bc2aa-113">Ajouter hello après les déclarations de variable après hello `require` instructions.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="bc2aa-114">Remplacez les valeurs d’espace réservé hello [Id de périphérique] et [clé de périphérique] avec les valeurs que vous avez pris note pour votre appareil dans hello distant solutions tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="bc2aa-115">Utilisez hello nom d’hôte du Hub IoT de hello solution du tableau de bord tooreplace [nom IoTHub].</span><span class="sxs-lookup"><span data-stu-id="bc2aa-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="bc2aa-116">Par exemple, si votre nom d’hôte IoT Hub est **contoso.azure-devices.net**, remplacez [Nom Hub IoT] par **contoso** :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="bc2aa-117">Ajoutez hello suivant variables toodefine certaines données de télémétrie de base :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="bc2aa-118">Ajoutez hello suivant des résultats de l’opération tooprint fonction d’assistance :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="bc2aa-119">Ajoutez hello d’assistance fonction toouse toorandomize hello télémétrie des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="bc2aa-120">Ajouter hello définition pourquoi **DeviceInfo** objet hello l’unité envoie au démarrage :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. <span data-ttu-id="bc2aa-121">Ajoutez hello suit définition pour le double de périphérique hello a signalé des valeurs.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="bc2aa-122">Cette définition inclut les descriptions des méthodes directes de hello hello périphérique prend en charge :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. <span data-ttu-id="bc2aa-123">Ajouter hello suivant hello toohandle de fonction **redémarrer** directe d’appel de méthode :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="bc2aa-124">Ajouter hello suivant hello toohandle de fonction **InitiateFirmwareUpdate** directe d’appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="bc2aa-125">Cette méthode directe utilise un emplacement de hello paramètre toospecify de toodownload d’image de microprogramme hello et lance hello mise à jour du microprogramme sur l’appareil de hello de façon asynchrone :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. <span data-ttu-id="bc2aa-126">Ajoutez hello suivant code toocreate une instance du client :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="bc2aa-127">Ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-127">Add hello following code to:</span></span>

    * <span data-ttu-id="bc2aa-128">Ouvrir une connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-128">Open hello connection.</span></span>
    * <span data-ttu-id="bc2aa-129">Envoyer hello **DeviceInfo** objet.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="bc2aa-130">Définir un gestionnaire pour les propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="bc2aa-131">Envoyer les propriétés signalées.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-131">Send reported properties.</span></span>
    * <span data-ttu-id="bc2aa-132">Inscrire des gestionnaires pour les méthodes directes hello.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="bc2aa-133">Démarrer l’envoi de la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-133">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. <span data-ttu-id="bc2aa-134">Enregistrer hello modifications toohello **remote_monitoring.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="bc2aa-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="bc2aa-135">Exécutez hello suivant de commande à partir d’un exemple d’application hello toolaunch invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="bc2aa-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
