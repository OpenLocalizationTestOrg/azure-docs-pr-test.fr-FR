---
title: aaaSimulate un appareil avec Azure IoT bord (Windows) | Documents Microsoft
description: "Comment toouse Azure IoT Edge sur Windows toocreate un appareil simulé qui envoie la télémesure via un hub IoT de Azure IoT bord passerelle tooan."
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
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="19e67-103">Utiliser des messages de périphérique dans le cloud Azure IoT bord toosend avec un appareil simulé (Windows)</span><span class="sxs-lookup"><span data-stu-id="19e67-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="19e67-104">Comment toorun hello exemple</span><span class="sxs-lookup"><span data-stu-id="19e67-104">How toorun hello sample</span></span>

<span data-ttu-id="19e67-105">Hello **build.cmd** script génère sa sortie dans hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="19e67-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="19e67-106">Cette sortie inclut quatre modules IoT bord hello, utilisées dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="19e67-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="19e67-107">Hello build script place le :</span><span class="sxs-lookup"><span data-stu-id="19e67-107">hello build script places the:</span></span>

* <span data-ttu-id="19e67-108">**Logger.dll** Bonjour **générer\\modules\\journal\\déboguer** dossier.</span><span class="sxs-lookup"><span data-stu-id="19e67-108">**logger.dll** in hello **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="19e67-109">**iothub.dll** Bonjour **générer\\modules\\iothub\\déboguer** dossier.</span><span class="sxs-lookup"><span data-stu-id="19e67-109">**iothub.dll** in hello **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="19e67-110">**identité\_map.dll** Bonjour **générer\\modules\\identitymap\\déboguer** dossier.</span><span class="sxs-lookup"><span data-stu-id="19e67-110">**identity\_map.dll** in hello **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="19e67-111">**simulé\_device.dll** Bonjour **générer\\modules\\simulé\_périphérique\\déboguer** dossier.</span><span class="sxs-lookup"><span data-stu-id="19e67-111">**simulated\_device.dll** in hello **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="19e67-112">Utilisez ces chemins d’accès pour hello **chemin du module** valeurs comme indiqué dans hello le fichier de paramètres JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="19e67-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="19e67-113">Hello simulée\_périphérique\_cloud\_télécharger\_exemple de processus prend le fichier de configuration hello chemin d’accès tooa JSON comme un argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="19e67-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="19e67-114">exemple de fichier JSON suivant Hello est fourni dans le référentiel du Kit de développement logiciel hello à **exemples\\simulé\_périphérique\_cloud\_télécharger\_exemple\\src\\ simulé\_périphérique\_cloud\_télécharger\_exemple\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="19e67-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="19e67-115">Ce fonctionne de fichier de configuration en l’état, sauf si vous modifiez hello construire des modules hello tooplace de script IoT bord ou un échantillon exécutables dans les emplacements par défaut.</span><span class="sxs-lookup"><span data-stu-id="19e67-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="19e67-116">le répertoire relatif toohello où hello simulée sont Hello chemins d’accès du module\_périphérique\_cloud\_télécharger\_sample.exe se trouve.</span><span class="sxs-lookup"><span data-stu-id="19e67-116">hello module paths are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="19e67-117">fichier de configuration JSON exemple Hello par défaut est toowriting too'deviceCloudUploadGatewaylog.log' dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="19e67-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="19e67-118">Dans un éditeur de texte, ouvrez le fichier de hello **exemples\\simulé\_périphérique\_cloud\_télécharger\_exemple\\src\\simulé\_périphérique \_cloud\_télécharger\_win.json** dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="19e67-118">In a text editor, open hello file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="19e67-119">Ce fichier configure les modules IoT bord hello dans l’exemple de passerelle hello :</span><span class="sxs-lookup"><span data-stu-id="19e67-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="19e67-120">Hello **IoTHub** module connecte tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="19e67-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="19e67-121">Vous configurer tooyour IoT hub toosend données.</span><span class="sxs-lookup"><span data-stu-id="19e67-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="19e67-122">Plus précisément, jeu hello **IoTHubName** valeur nom toohello de votre hub IoT et définir hello **IoTHubSuffix** valeur trop**azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="19e67-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="19e67-123">Ensemble hello **Transport** tooone de valeur de : **HTTP**, **AMQP**, ou **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="19e67-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="19e67-124">Actuellement, seul **HTTP** partage une connexion TCP pour tous les messages d’appareils.</span><span class="sxs-lookup"><span data-stu-id="19e67-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="19e67-125">Si la valeur hello trop**AMQP**, ou **MQTT**, passerelle de hello conserve un tooIoT connexion TCP de distinct concentrateur pour chaque périphérique.</span><span class="sxs-lookup"><span data-stu-id="19e67-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="19e67-126">Hello **mappage** module mappe les adresses MAC hello de votre ID d’appareil simulé appareils tooyour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="19e67-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="19e67-127">Assurez-vous que **deviceId** valeurs correspondance hello ID de hello deux périphériques que vous avez ajouté tooyour IoT hub et ce hello **deviceKey** valeurs contiennent des clés de hello de vos appareils de deux.</span><span class="sxs-lookup"><span data-stu-id="19e67-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="19e67-128">Hello **BLE1** et **BLE2** modules sont des périphériques de hello simulé.</span><span class="sxs-lookup"><span data-stu-id="19e67-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="19e67-129">Notez comment les adresses MAC hello module correspondent aux adresses hello Bonjour **mappage** module.</span><span class="sxs-lookup"><span data-stu-id="19e67-129">Note how hello module MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="19e67-130">Hello **journal** module connecte à votre fichier tooa d’activité passerelle.</span><span class="sxs-lookup"><span data-stu-id="19e67-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="19e67-131">Hello **chemin du module** hello l’exemple suivant montre les valeurs sont répertoire relatif toohello où hello simulée\_périphérique\_cloud\_télécharger\_sample.exe se trouve.</span><span class="sxs-lookup"><span data-stu-id="19e67-131">hello **module path** values shown in hello following example are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="19e67-132">Hello **liens** tableau bas hello du fichier JSON de hello connecte hello **BLE1** et **BLE2** modules toohello **mappage** module et hello **mappage** module toohello **IoTHub** module.</span><span class="sxs-lookup"><span data-stu-id="19e67-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="19e67-133">Cela garantit également que tous les messages sont enregistrés par hello **journal** module.</span><span class="sxs-lookup"><span data-stu-id="19e67-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

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

<span data-ttu-id="19e67-134">Enregistrez les modifications hello apportées toohello les fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="19e67-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="19e67-135">toorun hello, exemple :</span><span class="sxs-lookup"><span data-stu-id="19e67-135">toorun hello sample:</span></span>

1. <span data-ttu-id="19e67-136">À l’invite de commandes, accédez à toohello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="19e67-136">At a command prompt, navigate toohello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
2. <span data-ttu-id="19e67-137">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="19e67-137">Run hello following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="19e67-138">Vous pouvez utiliser hello [Explorateur de périphérique] [ lnk-device-explorer] ou [iothub-explorer] [ lnk-iothub-explorer] outil messages hello toomonitor IoT hub reçoit de hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="19e67-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="19e67-139">Par exemple, à l’aide de l’Explorateur du iothub vous pouvez surveiller les messages de périphérique dans le cloud à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="19e67-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="19e67-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19e67-140">Next steps</span></span>

<span data-ttu-id="19e67-141">toogain une plus grande maîtrise des IoT Edge et expérience avec quelques exemples de code, visitez hello développeur didacticiels et ressources :</span><span class="sxs-lookup"><span data-stu-id="19e67-141">toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="19e67-142">[Envoi de messages appareil-à-cloud à partir d’un appareil physique avec Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="19e67-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="19e67-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="19e67-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="19e67-144">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="19e67-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="19e67-145">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="19e67-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="19e67-146">[Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="19e67-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md