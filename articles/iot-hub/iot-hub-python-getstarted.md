---
title: aaaGet en main Azure IoT Hub (Python) | Documents Microsoft
description: "Découvrez comment toosend appareil-à-cloud messages tooAzure IoT Hub à l’aide de kits de développement logiciel IoT pour Python. Créer appareil simulé et tooregister des applications de service de votre appareil, envoyer des messages et lire les messages de hub IoT."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Connectez votre concentrateur de IoT tooyour appareil simulé à l’aide de Python
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

À la fin de hello de ce didacticiel, vous aurez deux applications Python :

* **CreateDeviceIdentity.py**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application d’appareil simulé.
* **SimulatedDevice.py**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, et régulièrement envoie une télémétrie de message à l’aide du protocole MQTT hello.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.
> 
> 

toocomplete ce didacticiel, vous devez hello suivant :

* [Python 2.x ou 3.x][lnk-python-download]. Assurez-vous que toouse hello 32 bits ou 64 bits l’installation en fonction des besoins de votre programme d’installation. Lorsque vous y êtes invité pendant l’installation de hello, rendre la variable d’environnement spécifiques à la plateforme tooyour à des Python tooadd sûr. Si vous utilisez Python 2.x, vous devrez peut-être trop[installer ou mettre à niveau *pip*, système de gestion de package hello Python][lnk-install-pip].
* Si vous utilisez le système d’exploitation Windows, puis [package redistribuable Visual C++] [ lnk-visual-c-redist] utilisation de hello tooallow de DLL natives à partir de Python.
* [Node.js 4.0 ou version ultérieure][lnk-node-download]. Assurez-vous que toouse hello 32 bits ou 64 bits l’installation en fonction des besoins de votre programme d’installation. Cela est nécessaire tooinstall hello [outil Explorateur de Hub IoT][lnk-iot-hub-explorer].
* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.

> [!NOTE]
> Hello *pip* packages pour `azure-iothub-service-client` et `azure-iothub-device-client` sont actuellement disponibles uniquement pour le système d’exploitation Windows. Pour Linux/Mac OS, reportez-vous à toohello des sections de Linux et Mac OS spécifiques sur hello [préparer votre environnement de développement Python] [ lnk-python-devbox] valider.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Votre IoT Hub est maintenant créé. Utilisez hello nom d’hôte IoT Hub et hello chaîne de connexion de IoT Hub reste hello de ce didacticiel.

> [!NOTE]
> Vous pouvez également créer facilement votre hub IoT sur une ligne de commande, à l’aide de hello Python ou Node.js basé CLI d’Azure. article de Hello [créez un IoT hub à l’aide de hello Azure CLI 2.0] [ lnk-azure-cli-hub] montre vous hello étapes rapides toodo donc. 
> 

## <a name="create-a-device-identity"></a>Création d’une identité d’appareil
Cette section répertorie hello étapes toocreate une application de console Python, qui crée une identité d’appareil dans le Registre des identités de votre hub IoT hello. Appareils de se connecter uniquement tooIoT Hub si elle a une entrée dans le Registre des identités hello. Pour plus d’informations, consultez hello **Registre des identités** section Hello [guide du développeur IoT Hub][lnk-devguide-identity]. Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub.

1. Ouvrez une invite de commandes et installer hello **Azure IoT Hub Service SDK pour Python**. Fermer l’invite de commandes hello après avoir installé hello SDK.

    ```
    pip install azure-iothub-service-client
    ```

2. Créez un fichier Python nommé **CreateDeviceIdentity.py**. Ouvrir dans [un éditeur/environnement IDE Python de votre choix][lnk-python-ide-list], par exemple, hello par défaut [inactif][lnk-idle].

3. Ajoutez hello suivant des modules de code tooimport hello requis à partir du service de hello SDK :

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Ajouter hello suivant de code, le remplacement d’espace réservé de hello pour `[IoTHub Connection String]` avec la chaîne de connexion hello pour hello IoT hub vous avez créé dans la section précédente de hello. Vous pouvez utiliser n’importe quel nom comme hello `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Ajouter hello après la fonction tooprint certaines des informations sur l’appareil hello.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Ajoutez hello suivant fonction toocreate hello appareil d’identification à l’aide de hello Gestionnaire du Registre. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Enfin, ajoutez fonction principale hello comme suit et enregistrer le fichier de hello.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. Sur l’invite de commandes hello, exécutez hello **CreateDeviceIdentity.py** comme suit :

    ```python
    python CreateDeviceIdentity.py
    ```
6. Vous devez voir les appareil simulé hello créé. Notez les hello **deviceId** et hello **primaryKey** de cet appareil. Vous avez besoin de ces valeurs lorsque vous créez une application qui se connecte tooIoT Hub en tant que périphérique.

    ![Création réussie de l’appareil][1]

> [!NOTE]
> Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé. Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et d’un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique. Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application. Pour plus d’informations, consultez hello [guide du développeur IoT Hub][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Cette section répertorie les étapes de hello toocreate une application de console Python, qui simule un appareil et envoie IoT hub tooyour de messages appareil-à-cloud.

1. Ouvrez une nouvelle invite de commande et installez hello Azure IoT Hub appareil SDK pour Python comme suit. Fermez l’invite de commandes hello après l’installation de hello.

    ```
    pip install azure-iothub-device-client
    ```
2. Créez un fichier nommé **SimulatedDevice.py**. Ouvrez ce fichier dans un éditeur/IDE Python de votre choix (par exemple, IDLE).

3. Ajoutez hello suivant des modules de code tooimport hello requis à partir de l’appareil hello SDK.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Ajouter le code suivant de hello et espace réservé de hello pour `[IoTHub Device Connection String]` avec la chaîne de connexion hello pour votre appareil. chaîne de connexion de périphérique Hello est généralement au format hello de `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Hello d’utilisation **deviceId** et **primaryKey** du périphérique hello vous avez créé dans hello de hello précédente section tooreplace `<deviceId>` et `<primaryKey>` respectivement. Remplacez `<hostName>` par le nom d’hôte de votre IoT Hub, généralement `<IoT hub name>.azure-devices.net`.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Ajoutez hello suivant code toodefine un rappel de confirmation d’envoi. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Ajoutez hello suivant du client de périphérique code tooinitialize hello.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Ajouter suivant de hello fonction tooformat et envoyer un message à partir de votre appareil simulé tooyour IoT de supervision.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Enfin, ajoutez les fonction principale hello. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Enregistrez et fermez hello **SimulatedDevice.py** fichier. Vous est désormais prêt toorun cette application.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Réception de messages à partir de votre appareil simulé
messages de télémétrie tooreceive à partir de votre appareil, vous devez toouse une [concentrateurs d’événements][lnk-event-hubs-overview]-point de terminaison compatible exposée par hello IoT Hub, qui lit les messages appareil-à-cloud hello. Hello de lecture [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel pour plus d’informations sur la manière dont les messages à partir de concentrateurs d’événements tooprocess pour le point de terminaison de votre hub IoT Hub d’événements compatibles. Concentrateurs d’événements ne prend pas en charge télémétrie dans Python encore, vous pouvez créer un [Node.js](iot-hub-node-node-getstarted.md#D2C_node) ou un [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) console basée sur les concentrateurs d’événements application tooread hello messages appareil-à-cloud à partir de IoT Hub. Ce didacticiel montre comment vous pouvez utiliser hello [outil Explorateur de Hub IoT] [ lnk-iot-hub-explorer] tooread ces messages de l’appareil.

1. Ouvrez une invite de commandes et installer hello IoT Hub Explorer. 

    ```
    npm install -g iothub-explorer
    ```

2. Exécutez hello commande suivante sur l’invite de commandes hello, toobegin analyse hello messages appareil-à-cloud à partir de votre appareil. Utilisez la chaîne de connexion de votre hub IoT dans l’espace réservé de hello après `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Ouvrez une nouvelle invite de commandes et accédez répertoire toohello contenant hello **SimulatedDevice.py** fichier.

4. Exécutez hello **SimulatedDevice.py** fichier, qui envoie périodiquement tooyour IoT hub de télémétrie des données. 
   
    ```
    python SimulatedDevice.py
    ```
5. Observez les messages d’appareil hello sur invite de commandes hello hello IoT Hub Explorer en cours d’exécution à partir de la section précédente de hello. 

    ![Messages appareil-à-cloud Python][2]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application toosend messages appareil-à-cloud toohello hub IoT. Vous observé les messages hello reçus par hello IoT hub à l’aide de hello de hello IoT Hub Explorateur. 

tooexplore hello Python SDK pour l’utilisation d’Azure IoT Hub en profondeur, visitez [ce référentiel Git Hub][lnk-python-github]. fonctionnalités de messagerie hello tooreview Hello Azure IoT Hub Service SDK pour Python, vous pouvez télécharger et exécuter [iothub_messaging_sample.py][lnk-messaging-sample]. Pour la simulation de côté l’appareil à l’aide de hello Azure IoT Hub appareil SDK pour Python, vous pouvez télécharger et exécuter hello [iothub_client_sample.py][lnk-client-sample].

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

* [Connexion de votre appareil][lnk-connect-device]
* [Prise en main de la gestion d’appareils][lnk-device-management]
* [Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Découvrir l’architecture Azure IoT Edge sur Linux)

toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
