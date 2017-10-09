---
title: aaaSimulate un appareil avec Azure IoT bord (Linux) | Documents Microsoft
description: "Comment toouse Azure IoT Edge sur Linux toocreate un appareil simulé qui envoie des données de télémétrie via un bord IoT IoT hub tooan de passerelle."
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
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="056a9-103">Utiliser des messages de périphérique dans le cloud Azure IoT bord toosend avec un appareil simulé (Linux)</span><span class="sxs-lookup"><span data-stu-id="056a9-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="056a9-104">Comment toorun hello exemple</span><span class="sxs-lookup"><span data-stu-id="056a9-104">How toorun hello sample</span></span>

<span data-ttu-id="056a9-105">Hello **build.sh** script génère sa sortie dans hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="056a9-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="056a9-106">Cette sortie inclut quatre modules IoT bord hello, utilisées dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="056a9-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="056a9-107">Hello build script place le :</span><span class="sxs-lookup"><span data-stu-id="056a9-107">hello build script places the:</span></span>

* <span data-ttu-id="056a9-108">**liblogger.so** Bonjour **/modules/journal de build** dossier.</span><span class="sxs-lookup"><span data-stu-id="056a9-108">**liblogger.so** in hello **build/modules/logger** folder.</span></span>
* <span data-ttu-id="056a9-109">**libiothub.so** Bonjour **build/modules/iothub** dossier.</span><span class="sxs-lookup"><span data-stu-id="056a9-109">**libiothub.so** in hello **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="056a9-110">**LIB\_identité\_map.so** Bonjour **build/modules/identitymap** dossier.</span><span class="sxs-lookup"><span data-stu-id="056a9-110">**lib\_identity\_map.so** in hello **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="056a9-111">**libsimulated\_device.so** Bonjour **build/modules/simulée\_périphérique** dossier.</span><span class="sxs-lookup"><span data-stu-id="056a9-111">**libsimulated\_device.so** in hello **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="056a9-112">Utilisez ces chemins d’accès pour hello **chemin du module** valeurs comme indiqué dans hello le fichier de paramètres JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="056a9-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="056a9-113">Hello simulée\_périphérique\_cloud\_télécharger\_exemple de processus prend le fichier de configuration hello chemin d’accès tooa JSON comme un argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="056a9-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="056a9-114">exemple de fichier JSON suivant Hello est fourni dans le référentiel du Kit de développement logiciel hello à **exemples\\simulé\_périphérique\_cloud\_télécharger\_exemple\\src\\ simulé\_périphérique\_cloud\_télécharger\_exemple\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="056a9-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="056a9-115">Ce fonctionne de fichier de configuration en l’état, sauf si vous modifiez hello construire des modules hello tooplace de script IoT bord ou un échantillon exécutables dans les emplacements par défaut.</span><span class="sxs-lookup"><span data-stu-id="056a9-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="056a9-116">chemins d’accès du module de Hello sont Active toohello relatif à partir duquel vous exécutez hello simulée\_périphérique\_cloud\_télécharger\_exécutable de l’exemple, pas le répertoire hello où se trouve le fichier exécutable de hello.</span><span class="sxs-lookup"><span data-stu-id="056a9-116">hello module paths are relative toohello directory from where you run hello simulated\_device\_cloud\_upload\_sample executable, not hello directory where hello executable is located.</span></span> <span data-ttu-id="056a9-117">fichier de configuration JSON exemple Hello par défaut est toowriting too'deviceCloudUploadGatewaylog.log' dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="056a9-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="056a9-118">Dans un éditeur de texte, ouvrez le fichier de hello **exemples/simulée\_périphérique\_cloud\_télécharger\_exemple/src/simulée\_périphérique\_cloud\_télécharger\_lin.json** dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="056a9-118">In a text editor, open hello file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="056a9-119">Ce fichier configure les modules IoT bord hello dans l’exemple de passerelle hello :</span><span class="sxs-lookup"><span data-stu-id="056a9-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="056a9-120">Hello **IoTHub** module connecte tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="056a9-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="056a9-121">Vous configurer tooyour IoT hub toosend données.</span><span class="sxs-lookup"><span data-stu-id="056a9-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="056a9-122">Plus précisément, jeu hello **IoTHubName** valeur nom toohello de votre hub IoT et définir hello **IoTHubSuffix** valeur trop**azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="056a9-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="056a9-123">Ensemble hello **Transport** tooone de valeur de : **HTTP**, **AMQP**, ou **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="056a9-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="056a9-124">Actuellement, seul **HTTP** partage une connexion TCP pour tous les messages d’appareils.</span><span class="sxs-lookup"><span data-stu-id="056a9-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="056a9-125">Si la valeur hello trop**AMQP**, ou **MQTT**, passerelle de hello conserve un tooIoT connexion TCP de distinct concentrateur pour chaque périphérique.</span><span class="sxs-lookup"><span data-stu-id="056a9-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="056a9-126">Hello **mappage** module mappe les adresses MAC hello de votre ID d’appareil simulé appareils tooyour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="056a9-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="056a9-127">Assurez-vous que **deviceId** valeurs correspondance hello ID de hello deux périphériques que vous avez ajouté tooyour IoT hub et ce hello **deviceKey** valeurs contiennent des clés de hello de vos appareils de deux.</span><span class="sxs-lookup"><span data-stu-id="056a9-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="056a9-128">Hello **BLE1** et **BLE2** modules sont des périphériques de hello simulé.</span><span class="sxs-lookup"><span data-stu-id="056a9-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="056a9-129">Notez comment leur MAC adresses correspondance hello adresses Bonjour **mappage** module.</span><span class="sxs-lookup"><span data-stu-id="056a9-129">Note how their MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="056a9-130">Hello **journal** module connecte à votre fichier tooa d’activité passerelle.</span><span class="sxs-lookup"><span data-stu-id="056a9-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="056a9-131">Hello **chemin du module** valeurs hello illustrés supposent que vous exécutez l’exemple hello de hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="056a9-131">hello **module path** values shown in hello example assume that you run hello sample from hello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
* <span data-ttu-id="056a9-132">Hello **liens** tableau bas hello du fichier JSON de hello connecte hello **BLE1** et **BLE2** modules toohello **mappage** module et hello **mappage** module toohello **IoTHub** module.</span><span class="sxs-lookup"><span data-stu-id="056a9-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="056a9-133">Cela garantit également que tous les messages sont enregistrés par hello **journal** module.</span><span class="sxs-lookup"><span data-stu-id="056a9-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

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

<span data-ttu-id="056a9-134">Enregistrez les modifications hello apportées toohello les fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="056a9-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="056a9-135">toorun hello, exemple :</span><span class="sxs-lookup"><span data-stu-id="056a9-135">toorun hello sample:</span></span>

1. <span data-ttu-id="056a9-136">Dans votre interpréteur de commandes, accédez à toohello **iot-bord/build** dossier.</span><span class="sxs-lookup"><span data-stu-id="056a9-136">In your shell, navigate toohello **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="056a9-137">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="056a9-137">Run hello following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="056a9-138">Vous pouvez utiliser hello [Explorateur de périphérique] [ lnk-device-explorer] ou [iothub-explorer] [ lnk-iothub-explorer] outil messages hello toomonitor IoT hub reçoit de hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="056a9-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="056a9-139">Par exemple, à l’aide de l’Explorateur du iothub vous pouvez surveiller les messages de périphérique dans le cloud à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="056a9-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="056a9-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="056a9-140">Next steps</span></span>

<span data-ttu-id="056a9-141">toogain une plus grande maîtrise de Azure IoT Edge et expérience avec quelques exemples de code, visitez hello développeur didacticiels et ressources :</span><span class="sxs-lookup"><span data-stu-id="056a9-141">toogain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="056a9-142">[Envoi de messages appareil-à-cloud à partir d’un appareil physique avec Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="056a9-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="056a9-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="056a9-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="056a9-144">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="056a9-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="056a9-145">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="056a9-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="056a9-146">[Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="056a9-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
