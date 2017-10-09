---
title: "aaaConnect un tooAzure passerelle IoT Suite à l’aide d’un NUC Intel | Documents Microsoft"
description: "Utilisez hello Microsoft IoT Commercial passerelle Kit et hello distant préconfigurée solution d’analyse. Utilisez Bonjour Azure IoT bord tooconnect toohello distant analyse de la solution, envoyer la télémétrie simulé toohello cloud et répondre toomethods appelé à partir du tableau de bord de solution hello."
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Se connecter à votre toohello de passerelle Azure IoT bord solution préconfigurée de surveillance à distance et d’envoyer la télémétrie simulé

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Ce didacticiel vous montre comment toouse Azure IoT bord toosimulate température et l’humidité données toosend toohello l’analyse à distance préconfiguré solution. didacticiel de Hello utilise :

- Un exemple de passerelle du tooimplement IoT bord Azure.
- la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.

## <a name="overview"></a>Vue d'ensemble

Dans ce didacticiel, vous effectuez hello comme suit :

- Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure. Cette étape déploie et configure automatiquement plusieurs services Azure.
- Configurer votre toocommunicate de périphérique de passerelle Intel NUC avec votre ordinateur et de la solution d’analyse à distance hello.
- Configurer hello IoT bord passerelle toosend simulée télémétrie que vous pouvez afficher sur le tableau de bord de solution hello.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure. déploiement de Hello reflète une architecture d’entreprise réel. frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui. Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Répétez hello précédentes étapes tooadd un deuxième appareil à l’aide d’un ID de périphérique comme **device02**. exemple Hello envoie des données à partir de deux appareils simulés dans hello passerelle toohello distant solution d’analyse.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script de compilation Hello place le module de IoT bord personnalisé hello libsimulator.so dans le dossier de génération hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurer et exécuter hello IoT passerelle

Vous pouvez maintenant configurer hello IoT bord passerelle toosend télémétrie simulé tooyour distant analyse du tableau de bord. Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> Dans ce didacticiel, vous utilisez standard de hello `vi` éditeur de texte sur hello NUC d’Intel. Si vous n’avez pas utilisé `vi` auparavant, vous devez effectuer un didacticiel d’introduction, telles que [Unix - hello vi didacticiel de l’éditeur] [ lnk-vi-tutorial] toofamiliarize vous-même avec cet éditeur. Vous pouvez également installer hello plus conviviaux [nano](https://www.nano-editor.org/) éditeur à l’aide de la commande hello `smart install nano -y`.

Fichier de configuration d’exemple hello ouvrir Bonjour **vi** éditeur à l’aide de hello de commande suivante :

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
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
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Remplacez hello **deviceID** et **deviceKey** des espaces réservés avec les identificateurs hello et des clés pour les appareils hello deux créé précédemment dans la solution d’analyse à distance hello.

Enregistrez vos modifications.

Vous pouvez maintenant exécuter hello IoT passerelle hello suivant à l’aide de commandes :

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

passerelle de Hello démarre sur hello Intel NUC et envoie la solution de surveillance à distance de télémétrie simulé toohello :

![La passerelle IoT Edge génère la télémétrie simulée][img-simulated telemetry]

Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.

## <a name="view-hello-telemetry"></a>Télémétrie des consultations de hello

Hello IoT passerelle envoie maintenant télémétrie simulé toohello une solution d’analyse à distance. Vous pouvez afficher les données de télémétrie hello sur le tableau de bord de solution hello.

- Accédez à tableau de bord toohello solution.
- Sélectionnez un des périphériques hello deux vous avez configuré dans la passerelle hello Bonjour **tooView de périphérique** liste déroulante.
- télémétrie Hello à partir des passerelles hello s’affiche sur le tableau de bord hello.

![Afficher les données de télémétrie des passerelles hello simulé][img-telemetry-display]

> [!WARNING]
> Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config]. Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.

## <a name="next-steps"></a>Étapes suivantes

Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started