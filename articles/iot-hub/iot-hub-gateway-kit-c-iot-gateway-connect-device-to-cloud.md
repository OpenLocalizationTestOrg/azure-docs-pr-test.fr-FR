---
title: aaaUse un tooconnect de passerelle un tooAzure appareil IoT Hub IoT | Documents Microsoft
description: "Découvrez comment toouse NUC Intel comme un tooconnect de passerelle IoT un SensorTag TI et envoi capteur données tooAzure IoT Hub Bonjour cloud."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "la passerelle est IOT connexion toocloud de périphérique"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>Utilisez IoT passerelle tooconnect choses toohello cloud - SensorTag tooAzure IoT Hub

> [!NOTE]
> Avant de commencer ce didacticiel, vérifiez que vous avez suivi le didacticiel [Configurer l’Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). Dans [configurer NUC Intel comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), vous configurez appareil d’Intel NUC hello comme passerelle IoT.

## <a name="what-you-will-learn"></a>Contenu

Vous apprendrez comment toouse un tooconnect de passerelle un tooAzure Texas Instruments SensorTag (CC2650STK) IoT Hub IoT. passerelle de IoT Hello envoie la température et de données de l’humidité collectés hello SensorTag tooAzure IoT Hub.

## <a name="what-you-will-do"></a>Procédure à suivre

- Créez un hub IoT.
- Inscrire un appareil dans hello IoT hub pour hello SensorTag.
- Activer des connexions entre la passerelle de IoT hello et hello SensorTag hello.
- Exécutez un ver exemple application toosend SensorTag tooyour IoT concentrateur de données.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Didacticiel [Configurer l’Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) suivi dans lequel vous configurez l’Intel NUC comme passerelle IoT.
- * Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
- Un client SSH qui s’exécute sur votre ordinateur hôte. PuTTY est recommandé sur Windows. Linux et macOS sont déjà accompagnés d’un client SSH.
- adresse IP de Hello et hello nom d’utilisateur et mot de passe tooaccess hello passerelle à partir du client SSH hello.
- Une connexion Internet.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Ici vous inscrivez ce nouvel appareil pour votre SensorTag

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Activer la connexion hello entre la passerelle de IoT hello et hello SensorTag

Dans cette section, vous effectuez hello tâches suivantes :

- Obtenir l’adresse MAC de hello Hello SensorTag pour connexion Bluetooth.
- Établir une connexion Bluetooth à partir de la passerelle toohello SensorTag de hello IoT.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Obtenir l’adresse MAC de hello Hello SensorTag pour connexion Bluetooth

1. Sur l’ordinateur hôte hello, exécutez hello SSH client et toohello IoT passerelle de connexion.
1. Débloquer Bluetooth en exécutant hello de commande suivante :

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Démarrer le service de Bluetooth hello sur la passerelle IoT hello et entrez un tooconfigure de shell Bluetooth Bluetooth en exécutant hello suivant de commandes :

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Contrôleur Bluetooth hello en cours d’exécution de mise sous tension hello commande à hello Bluetooth shell suivante :

   ```bash
   power on
   ```

   ![contrôleur de Bluetooth hello sur la passerelle IoT hello avec bluetoothctl mise sous tension](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Démarrer l’analyse pour à proximité d’appareils Bluetooth en exécutant hello de commande suivante :

   ```bash
   scan on
   ```

   ![Analyser les périphériques Bluetooth proches avec bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Appuyez sur hello bouton sur hello SensorTag d’appariement. Hello vert LED sur hello SensorTag clignote.
1. À hello Bluetooth shell, vous devez voir hello que sensortag est trouvé. Prenez note de hello adresse MAC de hello SensorTag. Dans cet exemple, hello adresse MAC de hello SensorTag est `24:71:89:C0:7F:82`.
1. Désactiver hello analyse en exécutant hello de commande suivante :

   ```bash
   scan off
   ```

   ![Arrêter l’analyse des périphériques Bluetooth proches avec bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Établir une connexion Bluetooth à partir de la passerelle toohello SensorTag de hello IoT

1. Se connecter toohello SensorTag en exécutant hello de commande suivante :

   ```bash
   connect <MAC address>
   ```

   ![Rejoignez toohello SensorTag bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Déconnectez hello SensorTag et quitter le shell de Bluetooth hello en hello suivant les commandes en cours d’exécution :

   ```bash
   disconnect
   exit
   ```

   ![Déconnectez hello SensorTag avec bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Vous avez activé connexion hello entre hello SensorTag et passerelle de IoT hello.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Exécuter un ver exemple application toosend SensorTag tooyour IoT concentrateur de données

Hello, exemple d’application Bluetooth faible énergie (tableau) est fournie par Azure IoT Edge. exemple d’application Hello collecte les données de connexion de l’activer et envoyer tooyou IoT hub hello données. toorun hello exemple d’application, vous devez :

1. Configurer l’application d’exemple hello.
1. Exécutez l’exemple d’application hello sur la passerelle IoT hello.

### <a name="configure-hello-sample-application"></a>Configurer l’application d’exemple hello

1. Accédez toohello le dossier de l’application d’exemple hello en exécutant hello de commande suivante :

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Ouvrez le fichier de configuration de hello en exécutant hello de commande suivante :

   ```bash
   vi ble_gateway.json
   ```

1. Dans le fichier de configuration de hello, renseignez hello valeurs suivantes :

   **IoTHubName**: nom hello de votre hub IoT.

   **IoTHubSuffix**: obtenir un IoTHubSuffix à partir de la clé primaire hello hello appareil de chaîne de connexion que vous avez notée vers le bas. Assurez-vous d’obtenir la clé primaire de hello de chaîne de connexion de périphérique hello, hello pas de clé primaire de votre chaîne de connexion de hub IoT. clé primaire de Hello de chaîne de connexion de périphérique hello est au format hello de `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Transport**: hello la valeur par défaut est `amqp`. Cette valeur indique le protocole de hello au cours de transpotation. Elle peut être `http`, `amqp` ou `mqtt`.

   **adresse Mac**: hello adresse MAC de hello SensorTag que vous avez notée vers le bas.

   **deviceID**: ID de périphérique hello que vous avez créé dans votre hub IoT.

   **deviceKey**: clé primaire de hello de chaîne de connexion de périphérique hello.

   ![Fichier de configuration complet hello Hello, exemple d’application BLE](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Appuyez sur `ESC` et type `:wq` fichier hello de toosave.

### <a name="run-hello-sample-application"></a>Exécutez l’exemple d’application hello

1. Vérifiez que hello que sensortag est sous tension.
1. Exécutez hello de commande suivante :

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Étapes suivantes

[Utiliser une passerelle IoT pour la transformation des données de capteur avec Azure IoT Edge](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
