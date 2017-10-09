> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Azure IoT Hub est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution. Didacticiels précédents ([prise en main IoT Hub] et [envoyer des messages Cloud-à-appareil avec IoT Hub]) illustrent hello appareil-à-cloud et cloud-à-appareil messagerie fonctionnalités de base d’IoT Hub. IoT Hub vous donne également hello des méthodes de non durables tooinvoke possibilité sur des périphériques de cloud de hello. Diriger les méthodes représentent une interaction de demande-réponse avec un tooan similaire de périphérique HTTP appeler dans la mesure où ils réussissent ou échouent immédiatement (après un délai d’attente spécifié par l’utilisateur) utilisateur de hello toolet savoir état hello d’appel de hello. [Appeler une méthode directe sur un appareil] [ lnk-devguide-methods] décrit plus en détail les méthodes directs et propose des conseils sur lorsque toouse directe des méthodes au lieu de messages cloud-à-appareil ou de propriétés souhaitées.

Ce didacticiel vous explique les procédures suivantes :

* Utilisez hello toocreate portail Azure un IoT hub et créer une identité d’appareil dans votre hub IoT.
* Créer une application d’appareil simulé qui possède une méthode directe qui peut être appelée par le cloud de hello.
* Créer une application console qui appelle une méthode directe dans l’application d’appareil simulé hello via votre hub IoT.

> [!NOTE]
> À ce stade, les méthodes directs sont uniquement pris en charge sur appareils qui se connectent à l’aide de concentrateur tooIoT hello protocole MQTT. Reportez-vous toohello [prise en charge MQTT] [ lnk-devguide-mqtt] article pour obtenir des instructions sur la façon de tooconvert existant appareil application toouse MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[envoyer des messages Cloud-à-appareil avec IoT Hub]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[prise en main IoT Hub]: ../articles/iot-hub/iot-hub-node-node-getstarted.md