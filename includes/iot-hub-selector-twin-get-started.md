> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

Les représentations d’appareil sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions). IoT Hub conserve un double du périphérique pour chaque périphérique qui se connecte tooit.

Vous pouvez utiliser des représentations d’appareil pour répondre aux besoins suivants :

* Stockez les métadonnées d’appareil à partir de votre serveur principal de solution.
* Rapports des informations d’état actuelles tels que conditions (par exemple, les méthode de connectivité de hello sont utilisée) et les fonctionnalités disponibles à partir de votre application.
* Synchroniser l’état hello de flux de travail longue (par exemple, les mises à jour de microprogramme et configuration) entre une application de périphérique et une application back-end.
* Interroger les métadonnées, la configuration ou l’état de vos appareils

> [!NOTE]
> Les représentations d’appareil sont conçues pour les synchronisations et pour l’interrogation des configurations et des conditions d’appareil. Plus d’informations sur quand jumeaux de périphérique toouse se trouvent dans [comprendre jumeaux de périphérique][lnk-twins].

Les représentations d’appareil sont stockées dans un IoT Hub et contiennent les éléments suivants :

* *balises*, les métadonnées de périphérique uniquement accessible hello solution back-end ;
* *propriétés souhaitée*, objets JSON modifiables par les solutions hello back-end et observable par application d’appareil hello ; et
* *signalé propriétés*, les objets JSON modifiables par l’application d’appareil hello et lisibles par hello solution back-end. Les étiquettes et les propriétés ne peuvent pas contenir de tableaux, mais les objets peuvent être imbriqués.

![][img-twin]

En outre, hello solution back-end peut interroger jumeaux appareil selon hello toutes les données.
Consultez trop[comprendre jumeaux de périphérique] [ lnk-twins] pour plus d’informations sur jumeaux de périphérique et toohello [langage de requête IoT Hub] [ lnk-query] référence pour l’interrogation.

> [!NOTE]
> À ce stade, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello. Reportez-vous toohello [prise en charge MQTT] [ lnk-devguide-mqtt] article pour obtenir des instructions sur la façon de tooconvert existant appareil application toouse MQTT.

Ce didacticiel vous explique les procédures suivantes :

* Créer une application back-end qui ajoute *balises* double de périphérique tooa et une application d’appareil simulé qui indique sa connectivité de canal en tant qu’un *signalé propriété* sur le double de périphérique hello.
* Interroger les périphériques à partir de votre application back-end à l’aide de filtres sur les balises de hello et de propriétés créées précédemment.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md