## <a name="create-a-device-identity"></a>Création d’une identité d’appareil

Dans cette section, vous utilisez un outil Node.js appelé [iothub-explorer] [ iot-hub-explorer] toocreate une identité d’appareil pour ce didacticiel. Les ID d’appareil respectent la casse.

1. Exécutez hello qui suit dans votre environnement de ligne de commande :

    `npm install -g iothub-explorer@latest`

1. Ensuite, exécutez hello suivant concentrateur de commande toologin tooyour. Substitution `{iot hub connection string}` avec hello chaîne de connexion de IoT Hub vous avez copiés précédemment :

    `iothub-explorer login "{iot hub connection string}"`

1. Enfin, créez une nouvelle identité d’appareil appelée `myDeviceId` avec la commande hello :

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Notez la chaîne de connexion de périphérique hello à partir du résultat de hello. Cette chaîne de connexion de périphérique est utilisée par l’application d’appareil hello tooyour tooconnect IoT Hub en tant que périphérique.

![][img-identity]

Consultez trop[prise en main de IoT Hub] [ lnk-getstarted] tooprogrammatically créer des identités de l’appareil.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
