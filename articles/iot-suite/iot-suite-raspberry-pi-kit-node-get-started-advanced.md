---
title: "met à jour des IoT Suite à l’aide de Node.js toosupport microprogramme aaaConnect un tooAzure framboises Pi | Documents Microsoft"
description: "Utilisez hello Microsoft Azure IoT Starter Kit pour hello framboises Pi 3 et Azure IoT Suite. Utiliser Node.js tooconnect votre solution de surveillance à distance de toohello framboises Pi, envoyer la télémétrie de capteurs toohello cloud et effectuer une mise à jour de microprogramme à distance."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a>Se connecter à votre solution de surveillance à distance de toohello framboises Pi 3 et activer les mises à jour de microprogramme à distance à l’aide de Node.js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Ce didacticiel vous montre comment toouse hello Microsoft Azure IoT Starter Kit pour framboises Pi 3 à :

* Développer un lecteur de température et humidité pouvant communiquer avec le cloud de hello.
* Activer et exécuter une application cliente hello de tooupdate de mise à jour du microprogramme à distance sur hello framboises Pi.

didacticiel de Hello utilise :

- Raspbian OS, hello Node.js langage de programmation et hello Microsoft Azure IoT SDK pour Node.js tooimplement un appareil de l’exemple.
- la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.

## <a name="overview"></a>Vue d'ensemble

Dans ce didacticiel, vous effectuez hello comme suit :

- Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure. Cette étape déploie et configure automatiquement plusieurs services Azure.
- Configurer votre toocommunicate capteurs et de périphérique avec votre ordinateur et le hello solution de surveillance à distance.
- Hello exemple périphérique code tooconnect toohello distant solution d’analyse de mise à jour et envoyer la télémétrie que vous pouvez afficher sur le tableau de bord de solution hello.
- Utilisez hello exemple périphérique code tooupdate hello d’application cliente.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure. déploiement de Hello reflète une architecture d’entreprise réel. frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui. Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

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

Si vous n’avez pas déjà fait, hello du clone requis référentiels en exécutant hello suivant de commandes sur votre Pi :

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Mettre à jour la chaîne de connexion de périphérique hello

Fichier de configuration d’exemple hello ouvrir Bonjour **nano** éditeur à l’aide de hello de commande suivante :

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Remplacez les valeurs d’espace réservé hello avec l’id de périphérique hello et informations IoT Hub vous avez créé et enregistré au démarrage hello de ce didacticiel.

Lorsque vous avez terminé, contenu hello du fichier deviceinfo de hello doit ressembler à hello l’exemple suivant :

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).

## <a name="run-hello-sample"></a>Exécuter l’exemple hello

Les commandes de suivantes de hello exécution tooinstall packages de composants requis hello pour exemple hello :

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

Vous pouvez maintenant exécuter l’exemple de programme hello sur hello framboises Pi. Entrez la commande hello :

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

Hello exemple de sortie suivant est un exemple de sortie hello, que reportez-vous à l’invite de commande hello sur hello framboises Pi :

![Sortie de l’application de Raspberry Pi][img-raspberry-output]

Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. Dans le tableau de bord hello solution, cliquez sur **périphériques** toovisit hello **périphériques** page. Sélectionnez votre Pi framboises Bonjour **liste des appareils**. Ensuite, choisissez **Méthodes** :

    ![Liste des appareils dans le tableau de bord][img-list-devices]

1. Sur hello **appeler une méthode** choisissez **InitiateFirmwareUpdate** Bonjour **méthode** liste déroulante.

1. Bonjour **FWPackageURI** , entrez **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**. Ce fichier contient l’implémentation de hello de la version 2.0 du microprogramme de hello.

1. Choisissez **InvokeMethod**. application Hello sur hello framboises Pi envoie un tableau de bord d’accusé de réception différé toohello solution. Il démarre ensuite le processus de mise à jour de microprogramme hello en téléchargeant hello nouvelle version du microprogramme de hello :

    ![Afficher l’historique de la méthode][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Observez le processus de mise à jour de microprogramme hello

Vous pouvez observer les processus de mise à jour de microprogramme hello lorsqu’elle s’exécute sur l’appareil de hello et que vous affichez hello signalés propriétés dans le tableau de bord de solution hello :

1. Vous pouvez afficher la progression hello dans des processus de mise à jour hello sur hello framboises Pi :

    ![Afficher la progression de la mise à jour][img-update-progress]

    > [!NOTE]
    > application de surveillance à distance Hello redémarre en mode silencieux lors de la mise à jour hello terminée. Utilisez la commande hello `ps -ef` tooverify, il est en cours d’exécution. Si vous souhaitez que le processus de hello tooterminate, utilisez hello `kill` avec l’id de processus hello.

1. Vous pouvez afficher le statut hello de mise à jour du microprogramme hello, comme indiqué par l’appareil de hello, dans le portail de solution hello. Hello capture d’écran suivante montre les état hello et durée de chaque étape du processus de mise à jour hello et la nouvelle version de microprogramme hello :

    ![Afficher l’état du travail][img-job-status]

    Si vous accédez à tableau de bord toohello précédent, vous pouvez vérifier le périphérique de hello envoie encore télémétrie après mise à jour du microprogramme hello.

> [!WARNING]
> Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config]. Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.

## <a name="next-steps"></a>Étapes suivantes

Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
