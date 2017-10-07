---
title: "aaaConnect un tooAzure framboises Pi IoT Suite à une télémétrie simulée à l’aide de Node.js | Documents Microsoft"
description: "Utilisez hello Microsoft Azure IoT Starter Kit pour hello framboises Pi 3 et Azure IoT Suite. Utiliser Node.js tooconnect votre solution de surveillance à distance de toohello framboises Pi, envoyer la télémétrie simulé toohello cloud et répondre toomethods appelée à partir du tableau de bord de solution hello."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a>Se connecter à votre solution de surveillance à distance de toohello framboises Pi 3 et envoyer la télémétrie simulé à l’aide de Node.js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Ce didacticiel vous montre comment toouse hello framboises Pi 3 toosimulate température et humidité données toosend toohello cloud. didacticiel de Hello utilise :

- Raspbian OS, hello Node.js langage de programmation et hello Microsoft Azure IoT SDK pour Node.js tooimplement un appareil de l’exemple.
- la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure. déploiement de Hello reflète une architecture d’entreprise réel. frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui. Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>Télécharger et configurer l’exemple hello

Vous pouvez maintenant télécharger et configurer l’application du client de contrôle à distance hello sur votre Pi framboises.

### <a name="install-nodejs"></a>Installer Node.js

Si vous ne l’avez pas déjà fait, installez Node.js sur votre Raspberry Pi. Hello IoT SDK pour Node.js nécessite 0.11.5 Node.js ou version ultérieure. Hello étapes suivantes vous montrent comment tooinstall les v6.10.2 de Node.js sur votre Pi framboises :

1. Utilisez hello suivant commande tooupdate votre Pi framboises :

    ```sh
    sudo apt-get update
    ```

1. Utilisez hello suivant commande toodownload hello Node.js binaires tooyour framboises Pi :

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Utilisez hello suivant des fichiers binaires de commande tooinstall hello :

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Utilisez hello suivant tooverify commande avoir installé Node.js v6.10.2 correctement :

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Clone hello référentiels

Si vous n’avez pas déjà fait, hello du clone requis référentiels en exécutant hello suivant de commandes dans un terminal de votre Pi :

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Mettre à jour la chaîne de connexion de périphérique hello

Fichier source d’exemple hello ouvrir Bonjour **nano** éditeur à l’aide de hello de commande suivante :

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Recherchez hello ligne :

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Remplacez les valeurs d’espace réservé hello par périphérique de hello et informations IoT Hub vous avez créé et enregistré au démarrage hello de ce didacticiel. Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).

## <a name="run-hello-sample"></a>Exécuter l’exemple hello

Les commandes de suivantes de hello exécution tooinstall packages de composants requis hello pour exemple hello :

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

Vous pouvez maintenant exécuter l’exemple de programme hello sur hello framboises Pi. Entrez la commande hello :

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Hello exemple de sortie suivant est un exemple de sortie hello, que reportez-vous à l’invite de commande hello sur hello framboises Pi :

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Étapes suivantes

Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
