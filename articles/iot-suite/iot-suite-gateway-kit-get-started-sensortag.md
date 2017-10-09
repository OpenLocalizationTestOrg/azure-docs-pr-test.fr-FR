---
title: "aaaConnect un tooAzure passerelle IoT Suite à l’aide d’un NUC Intel | Documents Microsoft"
description: "Utilisez hello Microsoft IoT Commercial passerelle Kit et hello distant préconfigurée solution d’analyse. Utilisez hello Azure IoT bord passerelle tooenable un SensorTag périphérique tooconnect toohello solution de surveillance à distance, envoyer cloud toohello de télémétrie et répondre toomethods appelée à partir du tableau de bord de solution hello."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Se connecter à votre toohello de passerelle Azure IoT bord solution préconfigurée de surveillance à distance et d’envoyer la télémétrie à partir d’un SensorTag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Ce didacticiel vous montre comment toouse Azure IoT toosend température et humidité données à partir de la surveillance à distance de SensorTag périphérique toohello solution préconfigurée. Hello SensorTag connecte la passerelle d’Intel NUC toohello à l’aide de Bluetooth. didacticiel de Hello utilise :

- Un exemple de passerelle du tooimplement IoT bord Azure.
- la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.

## <a name="overview"></a>Vue d'ensemble

Dans ce didacticiel, vous effectuez hello comme suit :

- Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure. Cette étape déploie et configure automatiquement plusieurs services Azure.
- Configurer votre toocommunicate de périphérique de passerelle Intel NUC avec votre ordinateur et de la solution d’analyse à distance hello.
- Configurer vos données de télémétrie Intel NUC passerelle tooreceive à partir d’un appareil SensorTag et envoyez-le toohello du tableau de bord de surveillance à distance.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas Instruments BLE SensorTag][lnk-sensortag]. Ce didacticiel récupère les données de télémétrie par Bluetooth à partir de l’appareil de SensorTag hello.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure. déploiement de Hello reflète une architecture d’entreprise réel. frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui. Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Configurer la connectivité Bluetooth

Configurer le Bluetooth sur hello Intel NUC tooenable hello SensorTag périphérique tooconnect et envoyer la télémétrie.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Rechercher l’adresse MAC de hello Hello SensorTag

1. Dans l’interface hello sur hello Intel NUC, exécutez hello après commande toounblock hello Bluetooth service :

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Suivante d’exécution hello commandes service Bluetooth hello Intel NUC toostart hello et entrez l’interpréteur de commandes hello Bluetooth :

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Exécutez hello suivant toopower de commande sur le contrôleur de hello Bluetooth :

    ```bash
    power on
    ```

    Lorsque le contrôleur de hello est activé, vous voyez un message **réussi de la modification de la puissance sur**.

1. Exécutez hello suivant tooscan de commande pour les périphériques Bluetooth à proximité :

    ```bash
    scan on
    ```

1. Appuyez sur hello bouton d’alimentation sur hello SensorTag toomake il détectable. DEL de Hello vert clignote.

1. Lorsque vous voyez un message dans le shell hello ce contrôleur hello a découvert hello SensorTag, prenez note de l’adresse MAC du périphérique de hello de hello. adresse MAC de Hello ressemble à **A0:E6:F8:B5:F6:00**. Vous devez adresse MAC de hello plus loin dans le didacticiel de hello lorsque vous configurez la passerelle de hello.

1. Exécutez hello suivant tooturn commande Désactiver Bluetooth analyse :

    ```bash
    scan off
    ```

1. Exécutez hello suivant tooverify de commande que vous pouvez vous connecter à toohello SensorTag appareil :

    ```bash
    connect <SensorTag MAC address>
    ```

    Si vous vous connectez avec succès, interpréteur de commandes hello affiche le message de type hello **connexion réussie** et imprime les informations sur l’appareil de SensorTag hello. Si vous ne pouvez pas vous connecter, vérifiez hello que sensortag est toujours sous tension.

1. Vous pouvez maintenant déconnecter hello SensorTag et quitter le shell de Bluetooth hello en hello suivant les commandes en cours d’exécution :

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Génération du module de IoT bord hello personnalisé

Vous pouvez à présent générer hello IoT bord module personnalisé qui permet de hello passerelle toosend messages toohello distant solution d’analyse. Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].

Télécharger le code de source de hello pour les modules de IoT bord hello personnalisés à partir de GitHub à l’aide de hello suivant de commandes :

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Génération du module IoT bord personnalisé de hello, à l’aide de hello suivant de commandes :

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script de compilation Hello place le module de IoT bord personnalisé hello libsensor2remotemonitoring.so dans le dossier de génération hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurer et exécuter hello IoT passerelle

Vous pouvez désormais configurer hello télémétrie de toosend passerelle IoT bord à partir de votre tooyour de périphérique SensorTag du tableau de bord de surveillance à distance. Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> Dans ce didacticiel, vous utilisez standard de hello `vi` éditeur de texte sur hello NUC d’Intel. Si vous n’avez pas utilisé `vi` auparavant, vous devez effectuer un didacticiel d’introduction, telles que [Unix - hello vi didacticiel de l’éditeur] [ lnk-vi-tutorial] toofamiliarize vous-même avec cet éditeur. Vous pouvez également installer hello plus conviviaux [nano](https://www.nano-editor.org/) éditeur à l’aide de la commande hello `smart install nano -y`.

Fichier de configuration d’exemple hello ouvrir Bonjour **vi** éditeur à l’aide de hello de commande suivante :

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

Recherchez hello lignes dans la configuration de hello pour le module de IoTHub hello suivantes :

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Remplacez l’espace réservé de hello valeurs hello informations IoT Hub vous avez créé et enregistré à hello Démarrer de ce didacticiel. valeur Hello pour IoTHubName ressemble à **yourrmsolution37e08**, et la valeur hello pour IoTSuffix est généralement **azure-devices.net**.

Recherchez hello lignes dans la configuration de hello pour le module de mappage hello suivantes :

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Remplacez hello **macAddress** espace réservé par hello adresse MAC de votre SensorTag que vous avez notée précédemment. Remplacez hello **deviceID** et **deviceKey** des espaces réservés avec les identificateurs hello et des clés pour les appareils hello deux créé précédemment dans la solution d’analyse à distance hello.

Recherchez hello lignes dans la configuration de hello pour le module de SensorTag hello suivantes :

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Remplacez hello **périphérique\_mac\_adresse** espace réservé par hello adresse MAC de votre SensorTag que vous avez notée précédemment.

Enregistrez vos modifications.

Vous pouvez maintenant exécuter passerelle hello hello suivant les commandes à l’aide de :

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Hello IoT passerelle démarre sur hello Intel NUC et envoie des données de télémétrie à partir de hello SensorTag toohello une solution d’analyse à distance :

![Passerelle IoT envoie des données de télémétrie à partir de hello SensorTag][img-telemetry]

Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.

## <a name="view-hello-telemetry"></a>Télémétrie des consultations de hello

passerelle de Hello envoie maintenant télémétrie à partir de hello SensorTag périphérique toohello distante solution d’analyse. Vous pouvez afficher les données de télémétrie hello sur le tableau de bord de solution hello. Vous pouvez également envoyer des périphériques de SensorTag tooyour commandes via la passerelle de hello à partir du tableau de bord de solution hello.

- Accédez à tableau de bord toohello solution.
- APPAREIL hello sélectionnez vous avez configuré dans la passerelle hello représentant hello SensorTag Bonjour **tooView de périphérique** liste déroulante.
- télémétrie Hello à partir de l’appareil de SensorTag hello s’affiche sur le tableau de bord hello.

![Afficher les données de télémétrie des appareils de SensorTag hello][img-telemetry-display]

> [!WARNING]
> Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config]. Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.


## <a name="next-steps"></a>Étapes suivantes

Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started