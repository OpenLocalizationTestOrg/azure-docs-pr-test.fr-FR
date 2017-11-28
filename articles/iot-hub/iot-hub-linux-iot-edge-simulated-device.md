---
title: Simuler un appareil avec Azure IoT Edge (Windows) | Documents Microsoft
description: "Comment utiliser le Kit de développement logiciel (SDK) de la passerelle Azure IoT sous Windows pour créer un appareil simulé qui envoie les données de télémétrie à un Azure IoT Hub via une passerelle."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 5349960373ae6815862c5f79a69dd6d5d9d624ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="5c8f2-103">Utilisation d’Azure IoT Edge pour envoyer des messages appareil-à-cloud avec un appareil simulé (Linux)</span><span class="sxs-lookup"><span data-stu-id="5c8f2-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="5c8f2-104">Comment exécuter l’exemple</span><span class="sxs-lookup"><span data-stu-id="5c8f2-104">How to run the sample</span></span>

<span data-ttu-id="5c8f2-105">Le script **build.sh** génère sa sortie dans le dossier **build** de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="5c8f2-106">Cette sortie inclut les quatre modules IoT Edge utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="5c8f2-107">Le script build place les fichiers comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-107">The build script places the:</span></span>

* <span data-ttu-id="5c8f2-108">**liblogger.so** dans le dossier **build/modules/logger**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-108">**liblogger.so** in the **build/modules/logger** folder.</span></span>
* <span data-ttu-id="5c8f2-109">**libiothub.so** dans le dossier **build/modules/iothub**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-109">**libiothub.so** in the **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="5c8f2-110">**lib\_identity\_map.so** dans le dossier **build/modules/identitymap**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-110">**lib\_identity\_map.so** in the **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="5c8f2-111">**libsimulated\_device.so** dans le dossier **build/modules/simulated\_device**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-111">**libsimulated\_device.so** in the **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="5c8f2-112">Utilisez ces chemins pour les valeurs **module path** comme indiqué dans le fichier de paramètres JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="5c8f2-113">Le processus simulated\_device\_cloud\_upload\_sample utilise le chemin vers un fichier de configuration JSON comme argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="5c8f2-114">L’exemple de fichier JSON suivant est fourni dans le référentiel du Kit de développement logiciel, sous **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="5c8f2-115">Ce fichier de configuration fonctionne comme tel, sauf si vous modifiez le script build pour placer des modules IoT Edge ou des exécutables de l’exemple dans des emplacements autres que ceux par défaut.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="5c8f2-116">Les chemins d’accès du module sont relatifs au répertoire à partir duquel vous exécutez l’exécutable simulated\_device\_cloud\_upload\_sample, et non au répertoire où se trouve l’exécutable.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-116">The module paths are relative to the directory from where you run the simulated\_device\_cloud\_upload\_sample executable, not the directory where the executable is located.</span></span> <span data-ttu-id="5c8f2-117">L’exemple de fichier de configuration JSON écrit par défaut dans « deviceCloudUploadGatewaylog.log » dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="5c8f2-118">Dans un éditeur de texte, ouvrez le fichier **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** dans votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-118">In a text editor, open the file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="5c8f2-119">Ce fichier configure les modules IoT Edge dans l'exemple de passerelle :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="5c8f2-120">Le module **IoTHub** se connecte à votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="5c8f2-121">Vous le configurez pour envoyer des données à votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="5c8f2-122">Plus précisément, définissez la valeur **IoTHubName** sur le nom de votre IoT Hub et la valeur **IoTHubSuffix** sur **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="5c8f2-123">Définissez la valeur de **Transport** sur **HTTP**, **AMQP** ou **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="5c8f2-124">Actuellement, seul **HTTP** partage une connexion TCP pour tous les messages d’appareils.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="5c8f2-125">Si vous définissez la valeur sur **AMQP** ou **MQTT**, la passerelle gère une connexion TCP à IoT Hub distincte pour chaque appareil.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="5c8f2-126">Le module **mapping** mappe les adresses MAC des appareils simulés aux ID de vos appareils IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="5c8f2-127">Assurez-vous que les valeurs **deviceId** correspondent aux ID des deux appareils que vous avez ajoutés à votre IoT Hub et que les valeurs **deviceKey** contiennent les clés de vos deux appareils.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="5c8f2-128">Les modules **BLE1** et **BLE2** sont les appareils simulés.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="5c8f2-129">Notez comment leurs adresses MAC correspondent à celles du module **mapping**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-129">Note how their MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="5c8f2-130">Le module **Logger** consigne l’activité de votre passerelle dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="5c8f2-131">Les valeurs **module path** affichées dans l’exemple supposent que vous exécuterez l’exemple à partir du dossier **build** de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-131">The **module path** values shown in the example assume that you run the sample from the **build** folder in your local copy of the **iot-edge** repository.</span></span>
* <span data-ttu-id="5c8f2-132">Le tableau **links** à la fin du fichier JSON se connecte les modules **BLE1** et **BLE2** au module **mapping**, et le module **mapping** au module **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="5c8f2-133">Il garantit également que tous les messages sont consignés par le module **Logger** .</span><span class="sxs-lookup"><span data-stu-id="5c8f2-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
            }
            },
            "args": {
              "IoTHubName": "<<insert here IoTHubName>>",
              "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
              "Transport": "HTTP"
            }
          },
        {
            "name": "mapping",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/identitymap/libidentity_map.so"
            }
            },
            "args": [
              {
                "macAddress": "01:01:01:01:01:01",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              },
              {
                "macAddress": "02:02:02:02:02:02",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              }
            ]
          },
        {
            "name": "BLE1",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "01:01:01:01:01:01"
            }
          },
        {
            "name": "BLE2",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "02:02:02:02:02:02"
            }
          },
        {
            "name": "Logger",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

<span data-ttu-id="5c8f2-134">Enregistrez les modifications apportées au fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="5c8f2-135">Pour exécuter l'exemple :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-135">To run the sample:</span></span>

1. <span data-ttu-id="5c8f2-136">Dans votre interpréteur de commandes, accédez au dossier **iot-edge/build**.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-136">In your shell, navigate to the **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="5c8f2-137">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-137">Run the following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="5c8f2-138">Vous pouvez utiliser l’outil [Explorateur d’appareils][lnk-device-explorer] ou [iothub-explorer][lnk-iothub-explorer] pour analyser les messages qu’IoT Hub reçoit de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="5c8f2-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="5c8f2-139">Par exemple, à l’aide d’iothub-explorer, vous pouvez surveiller les messages appareil-à-cloud à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="5c8f2-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c8f2-140">Next steps</span></span>

<span data-ttu-id="5c8f2-141">Pour approfondir vos connaissances sur Azure IoT Edge et découvrir certains exemples de code, consultez les didacticiels de développement et les ressources suivants :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-141">To gain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="5c8f2-142">[Envoi de messages appareil-à-cloud à partir d’un appareil physique avec Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="5c8f2-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="5c8f2-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="5c8f2-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="5c8f2-144">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="5c8f2-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5c8f2-145">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5c8f2-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5c8f2-146">[Sécuriser votre solution IoT de bout en bout][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5c8f2-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
