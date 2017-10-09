> [!div class="op_single_selector"]
> * [Device: Node.js Service: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Device: Node.js Service: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Appareil : service Java : Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Les applications de principal peuvent utiliser des primitives de Azure IoT Hub, telles que [double de l’appareil] [ lnk-devtwin] et [direct de méthodes][lnk-c2dmethod], tooremotely démarrer et surveiller actions de gestion de périphérique sur les appareils. Ce didacticiel vous montre comment une application back-end et une application de périphérique fonctionnent ensemble tooinitiate et surveiller un redémarrage de l’appareil à distance à l’aide de IoT Hub.

Utilisez un actions de gestion du périphérique tooinitiate méthode directe (par exemple, le redémarrage, paramètres d’usine et mise à jour du microprogramme) à partir d’une application back-end dans le cloud de hello. Appareil de Hello est responsable de :

* Gestion de demande de la méthode hello envoyé à partir de IoT Hub.
* Lancement hello spécifique au périphérique action correspondante sur les appareils hello.
* En fournissant des mises à jour d’état via *signalé propriétés* tooIoT Hub.

Vous pouvez utiliser une application back-end dans les requêtes hello cloud toorun appareil double tooreport progression hello de vos actions de gestion de périphérique.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
