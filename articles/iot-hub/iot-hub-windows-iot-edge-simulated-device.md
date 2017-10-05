---
title: Simuler un appareil avec Azure IoT Edge (Windows) | Microsoft Docs
description: "Comment utiliser Azure IoT Edge sous Windows pour créer un appareil simulé qui envoie les données de télémétrie à un IoT Hub via une passerelle IoT Edge."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: e7eb2931993daf3f0aecbd4a43d27ebd5adc10b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="5698c-103">Utilisation d’Azure IoT Edge pour envoyer des messages appareil-à-cloud avec un appareil simulé (Windows)</span><span class="sxs-lookup"><span data-stu-id="5698c-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="5698c-104">Comment exécuter l’exemple</span><span class="sxs-lookup"><span data-stu-id="5698c-104">How to run the sample</span></span>

<span data-ttu-id="5698c-105">Le script **build.cmd** génère sa sortie dans le dossier **build** de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5698c-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="5698c-106">Cette sortie inclut les quatre modules IoT Edge utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="5698c-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="5698c-107">Le script build place les fichiers comme suit :</span><span class="sxs-lookup"><span data-stu-id="5698c-107">The build script places the:</span></span>

* <span data-ttu-id="5698c-108">**logger.dll** dans le dossier **build\\modules\\logger\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="5698c-108">**logger.dll** in the **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="5698c-109">**iothub.dll** dans le dossier **build\\modules\\iothub\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="5698c-109">**iothub.dll** in the **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="5698c-110">**identity\_map.dll** dans le dossier **build\\modules\\identitymap\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="5698c-110">**identity\_map.dll** in the **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="5698c-111">**simulated\_device.dll** dans le dossier **build\\modules\\simulated\_device\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="5698c-111">**simulated\_device.dll** in the **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="5698c-112">Utilisez ces chemins pour les valeurs **module path** comme indiqué dans le fichier de paramètres JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="5698c-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="5698c-113">Le processus simulated\_device\_cloud\_upload\_sample utilise le chemin vers un fichier de configuration JSON comme argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5698c-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="5698c-114">L’exemple de fichier JSON suivant est fourni dans le référentiel du Kit de développement logiciel, sous **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="5698c-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="5698c-115">Ce fichier de configuration fonctionne comme tel, sauf si vous modifiez le script build pour placer des modules IoT Edge ou des exécutables de l’exemple dans des emplacements autres que ceux par défaut.</span><span class="sxs-lookup"><span data-stu-id="5698c-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="5698c-116">Les chemins de module sont relatifs au répertoire où se trouve le fichier simulated\_device\_cloud\_upload\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="5698c-116">The module paths are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="5698c-117">L’exemple de fichier de configuration JSON écrit par défaut dans « deviceCloudUploadGatewaylog.log » dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="5698c-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="5698c-118">Dans un éditeur de texte, ouvrez le fichier **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** dans votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5698c-118">In a text editor, open the file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="5698c-119">Ce fichier configure les modules IoT Edge dans l'exemple de passerelle :</span><span class="sxs-lookup"><span data-stu-id="5698c-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="5698c-120">Le module **IoTHub** se connecte à votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5698c-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="5698c-121">Vous le configurez pour envoyer des données à votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5698c-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="5698c-122">Plus précisément, définissez la valeur **IoTHubName** sur le nom de votre IoT Hub et la valeur **IoTHubSuffix** sur **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="5698c-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="5698c-123">Définissez la valeur de **Transport** sur **HTTP**, **AMQP** ou **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="5698c-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="5698c-124">Actuellement, seul **HTTP** partage une connexion TCP pour tous les messages d’appareils.</span><span class="sxs-lookup"><span data-stu-id="5698c-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="5698c-125">Si vous définissez la valeur sur **AMQP** ou **MQTT**, la passerelle gère une connexion TCP à IoT Hub distincte pour chaque appareil.</span><span class="sxs-lookup"><span data-stu-id="5698c-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="5698c-126">Le module **mapping** mappe les adresses MAC des appareils simulés aux ID de vos appareils IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5698c-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="5698c-127">Assurez-vous que les valeurs **deviceId** correspondent aux ID des deux appareils que vous avez ajoutés à votre IoT Hub et que les valeurs **deviceKey** contiennent les clés de vos deux appareils.</span><span class="sxs-lookup"><span data-stu-id="5698c-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="5698c-128">Les modules **BLE1** et **BLE2** sont les appareils simulés.</span><span class="sxs-lookup"><span data-stu-id="5698c-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="5698c-129">Notez comment les adresses MAC du module correspondent à celles du module **mapping**.</span><span class="sxs-lookup"><span data-stu-id="5698c-129">Note how the module MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="5698c-130">Le module **Logger** consigne l’activité de votre passerelle dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="5698c-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="5698c-131">Les valeurs **module path** figurant dans l’exemple suivant sont relatives au répertoire où se trouve le fichier simulated\_device\_cloud\_upload\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="5698c-131">The **module path** values shown in the following example are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="5698c-132">Le tableau **links** à la fin du fichier JSON se connecte les modules **BLE1** et **BLE2** au module **mapping**, et le module **mapping** au module **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="5698c-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="5698c-133">Il garantit également que tous les messages sont consignés par le module **Logger** .</span><span class="sxs-lookup"><span data-stu-id="5698c-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
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
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
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
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
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
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
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
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

<span data-ttu-id="5698c-134">Enregistrez les modifications apportées au fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="5698c-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="5698c-135">Pour exécuter l'exemple :</span><span class="sxs-lookup"><span data-stu-id="5698c-135">To run the sample:</span></span>

1. <span data-ttu-id="5698c-136">Accédez au dossier **build** de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5698c-136">At a command prompt, navigate to the **build** folder in your local copy of the **iot-edge** repository.</span></span>
2. <span data-ttu-id="5698c-137">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5698c-137">Run the following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="5698c-138">Vous pouvez utiliser l’outil [Explorateur d’appareils][lnk-device-explorer] ou [iothub-explorer][lnk-iothub-explorer] pour analyser les messages qu’IoT Hub reçoit de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="5698c-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="5698c-139">Par exemple, à l’aide d’iothub-explorer, vous pouvez surveiller les messages appareil-à-cloud à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5698c-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="5698c-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5698c-140">Next steps</span></span>

<span data-ttu-id="5698c-141">Pour approfondir vos connaissances sur Azure IoT Edge et découvrir certains exemples de code, consultez les didacticiels de développement et les ressources suivants :</span><span class="sxs-lookup"><span data-stu-id="5698c-141">To gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="5698c-142">[Envoi de messages appareil-à-cloud à partir d’un appareil physique avec Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="5698c-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="5698c-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="5698c-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="5698c-144">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="5698c-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5698c-145">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5698c-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5698c-146">[Sécuriser votre solution IoT de bout en bout][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5698c-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md