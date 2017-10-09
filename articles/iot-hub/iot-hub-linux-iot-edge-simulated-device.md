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
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a>Utiliser des messages de périphérique dans le cloud Azure IoT bord toosend avec un appareil simulé (Linux)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Comment toorun hello exemple

Hello **build.sh** script génère sa sortie dans hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel. Cette sortie inclut quatre modules IoT bord hello, utilisées dans cet exemple.

Hello build script place le :

* **liblogger.so** Bonjour **/modules/journal de build** dossier.
* **libiothub.so** Bonjour **build/modules/iothub** dossier.
* **LIB\_identité\_map.so** Bonjour **build/modules/identitymap** dossier.
* **libsimulated\_device.so** Bonjour **build/modules/simulée\_périphérique** dossier.

Utilisez ces chemins d’accès pour hello **chemin du module** valeurs comme indiqué dans hello le fichier de paramètres JSON suivant :

Hello simulée\_périphérique\_cloud\_télécharger\_exemple de processus prend le fichier de configuration hello chemin d’accès tooa JSON comme un argument de ligne de commande. exemple de fichier JSON suivant Hello est fourni dans le référentiel du Kit de développement logiciel hello à **exemples\\simulé\_périphérique\_cloud\_télécharger\_exemple\\src\\ simulé\_périphérique\_cloud\_télécharger\_exemple\_lin.json**. Ce fonctionne de fichier de configuration en l’état, sauf si vous modifiez hello construire des modules hello tooplace de script IoT bord ou un échantillon exécutables dans les emplacements par défaut.

> [!NOTE]
> chemins d’accès du module de Hello sont Active toohello relatif à partir duquel vous exécutez hello simulée\_périphérique\_cloud\_télécharger\_exécutable de l’exemple, pas le répertoire hello où se trouve le fichier exécutable de hello. fichier de configuration JSON exemple Hello par défaut est toowriting too'deviceCloudUploadGatewaylog.log' dans votre répertoire de travail actuel.

Dans un éditeur de texte, ouvrez le fichier de hello **exemples/simulée\_périphérique\_cloud\_télécharger\_exemple/src/simulée\_périphérique\_cloud\_télécharger\_lin.json** dans votre copie locale de hello **iot-bord** référentiel. Ce fichier configure les modules IoT bord hello dans l’exemple de passerelle hello :

* Hello **IoTHub** module connecte tooyour IoT hub. Vous configurer tooyour IoT hub toosend données. Plus précisément, jeu hello **IoTHubName** valeur nom toohello de votre hub IoT et définir hello **IoTHubSuffix** valeur trop**azure-devices.net**. Ensemble hello **Transport** tooone de valeur de : **HTTP**, **AMQP**, ou **MQTT**. Actuellement, seul **HTTP** partage une connexion TCP pour tous les messages d’appareils. Si la valeur hello trop**AMQP**, ou **MQTT**, passerelle de hello conserve un tooIoT connexion TCP de distinct concentrateur pour chaque périphérique.
* Hello **mappage** module mappe les adresses MAC hello de votre ID d’appareil simulé appareils tooyour IoT Hub. Assurez-vous que **deviceId** valeurs correspondance hello ID de hello deux périphériques que vous avez ajouté tooyour IoT hub et ce hello **deviceKey** valeurs contiennent des clés de hello de vos appareils de deux.
* Hello **BLE1** et **BLE2** modules sont des périphériques de hello simulé. Notez comment leur MAC adresses correspondance hello adresses Bonjour **mappage** module.
* Hello **journal** module connecte à votre fichier tooa d’activité passerelle.
* Hello **chemin du module** valeurs hello illustrés supposent que vous exécutez l’exemple hello de hello **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.
* Hello **liens** tableau bas hello du fichier JSON de hello connecte hello **BLE1** et **BLE2** modules toohello **mappage** module et hello **mappage** module toohello **IoTHub** module. Cela garantit également que tous les messages sont enregistrés par hello **journal** module.

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

Enregistrez les modifications hello apportées toohello les fichier de configuration.

toorun hello, exemple :

1. Dans votre interpréteur de commandes, accédez à toohello **iot-bord/build** dossier.
2. Exécutez hello de commande suivante :
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. Vous pouvez utiliser hello [Explorateur de périphérique] [ lnk-device-explorer] ou [iothub-explorer] [ lnk-iothub-explorer] outil messages hello toomonitor IoT hub reçoit de hello passerelle. Par exemple, à l’aide de l’Explorateur du iothub vous pouvez surveiller les messages de périphérique dans le cloud à l’aide de hello de commande suivante :

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Étapes suivantes

toogain une plus grande maîtrise de Azure IoT Edge et expérience avec quelques exemples de code, visitez hello développeur didacticiels et ressources :

* [Envoi de messages appareil-à-cloud à partir d’un appareil physique avec Azure IoT Edge][lnk-physical-device]
* [Azure IoT Edge][lnk-iot-edge]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
