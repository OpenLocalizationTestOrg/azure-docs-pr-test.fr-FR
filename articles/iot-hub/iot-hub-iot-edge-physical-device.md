---
title: aaaUse un appareil physique avec Azure IoT bord | Documents Microsoft
description: "Comment toouse un hub IoT Texas Instruments SensorTag périphérique toosend données tooan via une passerelle IoT en cours d’exécution sur un périphérique framboises Pi 3. passerelle de Hello est générée à l’aide de Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Utilisez Azure IoT bord sur un ordinateur framboises Pi tooforward messages appareil-à-cloud tooIoT Hub

Cette procédure pas à pas de hello [exemple de faible consommation d’énergie Bluetooth] [ lnk-ble-samplecode] vous montre comment toouse [Azure IoT bord] [ lnk-sdk] à :

* Transférer la télémétrie de l’appareil-à-cloud tooIoT Hub à partir d’un périphérique physique.
* Router les commandes à partir de l’unité physique de tooa IoT Hub.

Cette procédure pas à pas inclut les étapes suivantes :

* **Architecture**: architecture des informations importantes Bluetooth hello, exemple de faible consommation d’énergie.
* **Générez et exécutez**: toobuild de hello étapes requis et exemple hello d’exécution.

## <a name="architecture"></a>Architecture

procédure pas à pas Hello vous montre comment toobuild et exécuter une passerelle IoT sur un Pi framboises 3 qui exécute Raspbian Linux. passerelle de Hello est générée à l’aide de IoT Edge. exemple Hello utilise un Texas Instruments SensorTag Bluetooth faible énergie (BLE) périphérique toocollect température de données.

Lorsque vous exécutez hello IoT passerelle il :

* Connecte l’appareil de SensorTag de tooa à l’aide de protocole d’énergie de faible Bluetooth (BLE) hello.
* Se connecte tooIoT concentrateur à l’aide du protocole de hello HTTP.
* Transfère les données de télémétrie depuis hello SensorTag périphérique tooIoT Hub.
* Achemine les commandes à partir de l’appareil de SensorTag toohello IoT Hub.

passerelle de Hello contient hello suivant les modules IoT bord :

* A *module BLE* qui interagit avec un ver appareil tooreceive température de données à partir de hello et envoi commandes toohello périphérique.
* A *module BLE cloud toodevice* qui traduit les messages JSON envoyés à partir de IoT Hub en instructions BLE pour hello *module BLE*.
* A *module de l’enregistreur d’événements* enregistre tous les fichiers local passerelle messages tooa.
* Un *module de mappage d’identité* qui effectue la traduction entre les adresses MAC de l’appareil BLE et les identités des appareils Azure IoT Hub.
* Un *module de IoT Hub* qui télécharge tooan IoT hub de télémétrie des données et reçoit les commandes de l’appareil à partir d’un hub IoT.
* A *module d’imprimante BLE* qui interprète les données de télémétrie à partir de l’appareil BLE hello et imprime la résolution des problèmes de données mises en forme toohello console tooenable et de débogage.

### <a name="how-data-flows-through-hello-gateway"></a>Le flux des données via la passerelle de hello

Hello suivant le schéma illustre pipeline de flux de données hello télémétrie téléchargement :

![Pipeline de passerelle de téléchargement de télémétrie](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

étapes Hello qui un élément de données de télémétrie prend en déplacement à partir d’un tooIoT de périphérique BLE Hub sont :

1. APPAREIL BLE Hello génère un exemple de la température et l’envoie sur le module BLE toohello Bluetooth dans la passerelle de hello.
1. module BLE Hello reçoit l’exemple hello et le publie broker toohello, ainsi que l’adresse MAC de hello du périphérique de hello.
1. module de mappage d’identité Hello récupère ce message et utilise un hello tootranslate de table interne adresse MAC du périphérique de hello en une identité d’appareil IoT Hub. Une identité d’appareil IoT Hub se compose d’un ID d’appareil et d’une clé d’appareil.
1. module de mappage d’identité Hello publie un nouveau message qui contient les données d’exemple hello température, adresse MAC de hello du dispositif de hello, ID de périphérique hello et clé de périphérique hello.
1. Hello module de IoT Hub reçoit ce nouveau message (généré par le module de mappage d’identité hello) et le publie tooIoT Hub.
1. module d’enregistreur d’événements Hello enregistre tous les messages à partir de fichiers local de hello broker tooa.

Hello suivant le schéma illustre pipeline de flux de données hello appareil commande :

![Pipeline de passerelle de commande d’appareil](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Hello IoT Hub module interroge régulièrement hello IoT hub pour les nouveaux messages de commande.
1. Lorsque hello module de IoT Hub reçoit un nouveau message de commande, il publie toohello broker.
1. module de mappage d’identité Hello récupère le message de commande hello et utilise un hello tootranslate de table interne IoT Hub ID tooa périphérique adresse MAC. Il publie ensuite un nouveau message qui comprend des hello l’adresse MAC du périphérique cible de hello dans le mappage de propriétés hello de message de type hello.
1. module BLE Cloud-à-appareil Hello récupère ce message et le traduit en instruction BLE appropriée de hello pour le module BLE hello. Il publie ensuite un nouveau message.
1. module BLE Hello récupère ce message et exécute l’instruction d’e/s de hello en communiquant avec un périphérique BLE hello.
1. module d’enregistreur d’événements Hello enregistre tous les messages à partir du fichier de disque tooa hello broker.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.

> [!NOTE]
> Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].

Vous devez client SSH sur votre tooenable d’ordinateur de bureau vous tooremotely accès hello de ligne de commande sur hello framboises Pi.

- Windows n’inclut pas de client SSH. Nous vous recommandons d’utiliser [PuTTY](http://www.putty.org/).
- La plupart des distributions Linux et Mac OS incluent l’utilitaire SSH hello. Pour plus d’informations, consultez [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Utilisation de SSH avec Linux ou Mac OS).

## <a name="prepare-your-hardware"></a>Préparation du matériel

Ce didacticiel suppose que vous utilisez un [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) appareil connecté tooa framboises Pi 3 Raspbian en cours d’exécution.

### <a name="install-raspbian"></a>Installer Raspbian

Vous pouvez utiliser une des hello suivant les options tooinstall Raspbian sur votre appareil framboises Pi 3.

* version la plus récente hello tooinstall de Raspbian, utilisez hello [NOOBS] [ lnk-noobs] interface utilisateur graphique.
* Manuellement [télécharger] [ lnk-raspbian] et écrire la dernière image de hello de carte de hello Raspbian système d’exploitation tooan SD.

### <a name="sign-in-and-access-hello-terminal"></a>Se connecter et accéder à Terminal Server de hello

Vous avez deux options tooaccess d’un environnement de Terminal Server sur votre Pi framboises :

* Si vous possédez un clavier et surveillez tooyour connecté framboises Pi, vous pouvez utiliser hello Raspbian GUI tooaccess une fenêtre de terminal.

* Ligne de commande accès hello sur votre Pi framboises à l’aide de SSH à partir de votre ordinateur de bureau.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Utiliser une fenêtre de terminal dans l’interface graphique utilisateur de hello

informations d’identification par défaut de Hello pour Raspbian sont le nom d’utilisateur **pi** et le mot de passe **framboises**. Dans la barre des tâches hello Bonjour l’interface graphique utilisateur, vous pouvez lancer hello **Terminal** utility à l’aide d’icône hello qui ressemble à une analyse.

#### <a name="sign-in-with-ssh"></a>Se connecter avec SSH

Vous pouvez utiliser SSH pour l’accès en ligne de commande tooyour framboises Pi. article de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] décrit comment tooconfigure SSH sur votre Pi framboises et comment tooconnect de [Windows] [ lnk-ssh-windows] ou [Linux et Mac OS][lnk-ssh-linux].

Connectez-vous avec le nom d’utilisateur **pi** et le mot de passe **raspberry**.

### <a name="install-bluez-537"></a>Installer BlueZ 5.37

matériel de Bluetooth toohello via la pile de BlueZ hello communiquer avec les modules BLE Hello. Vous devez correctement version 5.37 de BlueZ pour toowork de modules hello. Ces instructions Assurez-vous hello la version correcte de BlueZ est installée.

1. Arrêter le démon de bluetooth hello actuel :

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Installer les dépendances de BlueZ hello :

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Télécharger le code de source de hello BlueZ de bluez.org :

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Décompressez le code source de hello :

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Changer le dossier répertoires toohello nouvellement créé :

    ```sh
    cd bluez-5.37
    ```

1. Configurer hello BlueZ code toobe généré :

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Générez BlueZ :

    ```sh
    make
    ```

1. Installez BlueZ une fois la génération terminée :

    ```sh
    sudo make install
    ```

1. Modifier la configuration service systemd pour bluetooth afin qu’il pointe toohello nouveau bluetooth démon dans le fichier de hello `/lib/systemd/system/bluetooth.service`. Remplacez ligne de 'ExecStart' hello hello suivant du texte :

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Activer la connectivité toohello SensorTag périphérique à partir de votre appareil framboises Pi 3

Avant d’en cours d’exécution exemple hello, vous devez tooverify que votre framboises Pi 3 peut se connecter toohello SensorTag appareil.

1. Assurez-vous de hello `rfkill` utilitaire est installé :

    ```sh
    sudo apt-get install rfkill
    ```

1. Débloquer bluetooth sur hello framboises Pi 3 et vérifier que le numéro de version de hello est **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. interpréteur de commandes tooenter hello bluetooth interactif, démarrer le service bluetooth hello et exécutez hello **bluetoothctl** commande :

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Entrez la commande hello **mise sous tension** toopower contrôleur bluetooth de hello. commande Hello retourne suivant toohello similaire de sortie :

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. Dans l’interpréteur de commandes interactive bluetooth hello, entrez la commande hello **analyse sur** tooscan pour les appareils bluetooth. commande Hello retourne suivant toohello similaire de sortie :

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Rendre les périphériques de SensorTag hello détectable en appuyant sur le bouton de petit hello (hello LED verte doit clignoter). Hello framboises Pi 3 doit découvrir un périphérique SensorTag hello :

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    Dans cet exemple, vous pouvez voir cette adresse MAC de hello SensorTag périphérique est hello **A0:E6:F8:B5:F6:00**.

1. Désactiver l’analyse en entrant hello **analyse désactivée** commande :

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Connecter l’appareil de SensorTag tooyour à l’aide de son adresse MAC en entrant **connecter \<adresse MAC\>**. Pour plus de clarté, Hello suivant l’exemple de sortie est abrégé :

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Vous pouvez répertorier les caractéristiques de GATT hello du périphérique hello à nouveau à l’aide de hello **-liste d’attributs** commande.

1. Vous pouvez désormais vous déconnecter d’appareil hello à l’aide de hello **déconnecter** de commandes, puis quittez à partir de l’interpréteur de commandes bluetooth hello à l’aide de hello **quitter** commande :

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

Vous êtes maintenant prêt toorun hello, exemple BLE IoT bord sur votre framboises Pi 3.

## <a name="run-hello-iot-edge-ble-sample"></a>Exécutez l’exemple de tableau de bord IoT hello

exemple de tableau de bord IoT toorun hello, vous devez toocomplete trois tâches :

* Configurer deux exemples d’appareils dans votre IoT Hub.
* Générer IoT Edge sur votre appareil Raspberry Pi 3.
* Configurer et exécuter l’exemple de tableau hello sur votre appareil framboises Pi 3.

Au moment de l’écriture de hello, IoT Edge prend uniquement en charge les modules de l’activer dans les passerelles en cours d’exécution sur Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Configuration de deux exemples d’appareils dans votre IoT Hub

* [Créez un hub IoT] [ lnk-create-hub] dans votre abonnement Azure, vous devez fournir hello nom de votre concentrateur de toocomplete cette procédure pas à pas. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* Ajouter un périphérique appelé **SensorTag_01** tooyour IoT hub et prenez note de sa clé d’id et de périphérique. Vous pouvez utiliser hello [Explorateur de l’appareil ou l’Explorateur de l’iothub] [ lnk-explorer-tools] outils tooadd ce hub IoT de toohello périphérique vous avez créé dans l’étape précédente de hello et tooretrieve sa clé. Vous mappez ce périphérique toohello SensorTag périphérique lorsque vous configurez la passerelle de hello.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Générer Azure IoT Edge sur votre appareil Raspberry Pi 3

Installer les dépendances pour Azure IoT Edge :

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

Des commandes suivantes de hello utilisation tooclone IoT Edge et tous les sous-modules tooyour répertoire de base :

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Quand vous avez une copie complète de hello référentiel de IoT bord sur votre framboises Pi 3, vous pouvez créer à l’aide de hello de commande suivante à partir du dossier hello contenant hello SDK :

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Configurer et exécuter l’exemple BLE de hello sur votre framboises Pi 3

toobootstrap et exemple hello exécution, vous devez configurer chaque module IoT Edge qui participe dans la passerelle de hello. Cette configuration est fournie dans un fichier JSON et vous devez configurer les cinq modules IoT Edge participants. Il est un exemple de fichier JSON dans le référentiel hello appelé **passerelle\_sample.json** que vous pouvez utiliser comme point de départ pour créer votre propre fichier de configuration de hello. Ce fichier est hello **ble_gateway/samples/src** dossier dans une copie locale de hello référentiel de IoT Edge.

Hello sections suivantes décrivent comment tooedit cette configuration du fichier pour l’exemple de tableau hello et supposent que référentiel de IoT bord hello est Bonjour **/home/pi/iot-edge /** dossier sur votre framboises Pi 3. Si le référentiel de hello se trouve ailleurs, ajuster en conséquence les chemins d’accès hello.

#### <a name="logger-configuration"></a>Configuration de l’enregistreur

En supposant que le référentiel de passerelle hello se trouve dans hello **/home/pi/iot-edge /** dossier, configurez le module d’enregistreur d’événements hello comme suit :

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>Configuration du module BLE

configuration d’exemple Hello pour appareil BLE hello suppose un appareil Texas Instruments SensorTag. N’importe quel appareil BLE standard qui peut fonctionner comme un périphérique de GATT doit fonctionner, mais vous devrez peut-être caractéristique de GATT hello tooupdate ID et les données. Ajouter une adresse MAC de hello de votre périphérique SensorTag :

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Si vous n’utilisez pas un appareil SensorTag, passez en revue documentation hello pour votre toodetermine de périphérique BLE si vous avez besoin de caractéristique de GATT hello tooupdate ID et les valeurs de données.

#### <a name="iot-hub-module"></a>module IoT Hub

Ajouter le nom hello de votre IoT Hub. valeur de suffixe Hello est généralement **azure-devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Configuration du mappage d’identité

Ajouter une adresse MAC de hello de SensorTag appareil et hello périphérique ID et votre clé de hello **SensorTag_01** appareil que vous avez ajouté tooyour IoT Hub :

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Configuration du module d’imprimante BLE

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>Configuration du module BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Configuration du routage

Hello configuration suivante garantit suivant de hello routage entre les modules IoT bord :

* Hello **journal** module reçoit et enregistre tous les messages.
* Hello **SensorTag** module envoie hello tooboth de messages **mappage** et **BLE imprimante** modules.
* Hello **mappage** module envoie des messages toohello **IoTHub** toobe module envoyé tooyour IoT Hub.
* Hello **IoTHub** module envoie des messages au toohello **mappage** module.
* Hello **mappage** module envoie des messages toohello **BLEC2D** module.
* Hello **BLEC2D** module envoie des messages au toohello **capteur balise** module.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

exemple hello de toorun, fichier configuration passe hello chemin d’accès toohello JSON comme un paramètre de toohello **ble\_passerelle** binaire. Hello commande suivante suppose que vous utilisez hello **gateway_sample.json** fichier de configuration. Exécutez la commande suivante à partir de hello **iot-bord** dossier hello framboises Pi :

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Vous devrez peut-être toopress hello petit bouton hello SensorTag périphérique toomake il détectables avant d’exécuter les exemples hello.

Lorsque vous exécutez hello, exemple, vous pouvez utiliser hello [Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [iothub-explorer](https://github.com/Azure/iothub-explorer) outil toomonitor Bonjour messages Bonjour IoT passerelle transfère à partir de l’appareil de SensorTag hello. Par exemple, à l’aide de l’Explorateur du iothub vous pouvez surveiller les messages de périphérique dans le cloud à l’aide de hello de commande suivante :

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Envoi de messages cloud vers appareil

module BLE Hello prend également en charge l’envoi de commandes à partir de l’appareil de toohello IoT Hub. Vous pouvez utiliser hello [Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [iothub-explorer](https://github.com/Azure/iothub-explorer) transfère les messages de l’outil toosend JSON ce module de passerelle BLE hello sur l’appareil BLE toohello.

Si vous utilisez un périphérique de Texas Instruments SensorTag hello, vous pouvez activer les DEL hello rouge, vert ou alarme sonore en envoyant des commandes à partir de IoT Hub. Avant d’envoyer des commandes à partir de IoT Hub, d’abord envoyer hello suivant deux messages JSON dans l’ordre. Ensuite, vous pouvez envoyer des tooturn de commandes hello sur les témoins lumineux de hello ou alarme sonore.

1. Réinitialiser tous les voyants et alarme sonore de hello (les mettre hors tension) :

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. Configurer les E/S en tant que « à distance » :

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

Vous pouvez maintenant envoyer des hello suivant de commandes tooturn sur les témoins lumineux de hello ou alarme sonore sur le périphérique de SensorTag hello :

* Activer les DEL hello rouge :

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Activer les DEL hello vert :

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Activer l’alarme sonore de hello :

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez toogain une plus grande maîtrise du bord de IoT et faire des essais avec quelques exemples de code, visitez hello développeur didacticiels et ressources :

* [Azure IoT Edge][lnk-sdk]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
