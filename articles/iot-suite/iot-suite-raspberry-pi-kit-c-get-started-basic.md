---
title: "aaaConnect un tooAzure framboises Pi IoT Suite à l’aide de C avec capteurs réels | Documents Microsoft"
description: "Utilisez hello Microsoft Azure IoT Starter Kit pour hello framboises Pi 3 et Azure IoT Suite. Utilisez C tooconnect votre solution de surveillance à distance de toohello framboises Pi, envoyer la télémétrie de capteurs toohello cloud et répondre toomethods appelée à partir du tableau de bord de solution hello."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a>Se connecter à votre solution de surveillance à distance de toohello framboises Pi 3 et envoyer la télémétrie à partir d’un capteur réels à l’aide de C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Ce didacticiel vous montre comment toouse hello Microsoft Azure IoT Starter Kit pour framboises Pi 3 toodevelop, un lecteur de température et humidité pouvant communiquer avec le cloud de hello. didacticiel de Hello utilise :

- Raspbian du système d’exploitation, langage de programmation hello C et hello Microsoft Azure IoT SDK pour C tooimplement un appareil de l’exemple.
- la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.

## <a name="overview"></a>Vue d'ensemble

Dans ce didacticiel, vous effectuez hello comme suit :

- Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure. Cette étape déploie et configure automatiquement plusieurs services Azure.
- Configurer votre toocommunicate capteurs et de périphérique avec votre ordinateur et le hello solution de surveillance à distance.
- Hello exemple périphérique code tooconnect toohello distant solution d’analyse de mise à jour et envoyer la télémétrie que vous pouvez afficher sur le tableau de bord de solution hello.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure. déploiement de Hello reflète une architecture d’entreprise réel. frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui. Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Télécharger et configurer l’exemple hello

Vous pouvez maintenant télécharger et configurer l’application du client de contrôle à distance hello sur votre Pi framboises.

### <a name="clone-hello-repositories"></a>Clone hello référentiels

Si vous n’avez pas déjà fait, hello du clone requis référentiels en exécutant hello suivant de commandes dans un terminal de votre Pi :

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a>Mettre à jour la chaîne de connexion de périphérique hello

Fichier source d’exemple hello ouvrir Bonjour **nano** éditeur à l’aide de hello de commande suivante :

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

Recherchez hello lignes suivantes :

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Remplacez les valeurs d’espace réservé hello par périphérique de hello et informations IoT Hub vous avez créé et enregistré au démarrage hello de ce didacticiel. Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).

## <a name="build-hello-sample"></a>Générez l’exemple hello

Installer les packages de composants requis hello pour hello Kit de développement logiciel de Microsoft Azure IoT appareil pour C en exécutant hello suivant de commandes dans un terminal de hello framboises Pi :

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Vous pouvez ensuite générer la solution de l’exemple hello mis à jour sur hello framboises Pi :

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

Vous pouvez maintenant exécuter l’exemple de programme hello sur hello framboises Pi. Entrez la commande hello :

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Hello exemple de sortie suivant est un exemple de sortie hello, que reportez-vous à l’invite de commande hello sur hello framboises Pi :

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Étapes suivantes

Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
