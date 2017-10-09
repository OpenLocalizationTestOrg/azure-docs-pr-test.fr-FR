---
title: aaaUnderstand prise en charge Azure IoT Hub MQTT | Documents Microsoft
description: "Développeur guide - prise en charge des appareils qui se connectent tooan à l’aide de point de terminaison IoT Hub périphérique hello protocole MQTT. Contient des informations sur la prise en charge intégrée de MQTT Bonjour kits de développement logiciel Azure IoT appareil."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Communiquer avec votre IoT hub à l’aide du protocole MQTT hello

IoT Hub permet de périphériques toocommunicate avec points de terminaison appareil de Hub IoT hello à l’aide de hello [MQTT v3.1.1] [ lnk-mqtt-org] protocole sur le port 8883 ou v3.1.1 MQTT via le protocole WebSocket sur le port 443. IoT Hub nécessite tous les toobe de communication de périphérique sécurisé à l’aide de TLS/SSL (donc IoT Hub ne prend en charge des connexions non sécurisées sur le port 1883).

## <a name="connecting-tooiot-hub"></a>Connexion tooIoT Hub

Un périphérique peut utiliser l’hello MQTT protocole tooconnect tooan IoT hub à l’aide de bibliothèques hello Bonjour [kits de développement logiciel Azure IoT] [ lnk-device-sdks] ou en utilisant le protocole MQTT hello directement.

## <a name="using-hello-device-sdks"></a>À l’aide de l’appareil hello kits de développement logiciel

[Kits de développement logiciel appareil] [ lnk-device-sdks] que hello prise en charge de protocole MQTT sont disponibles pour Java, Node.js, C, C# et Python. l’appareil Hello kits de développement logiciel utiliser hello standard IoT Hub connexion chaîne tooestablish un IoT hub de connexion tooan. protocole MQTT toouse hello, paramètre de protocole de hello client doit être défini trop**MQTT**. Par défaut, le périphérique hello kits de développement logiciel se connecter tooan IoT Hub hello **CleanSession** indicateur défini trop**0** et utiliser **QoS 1** pour l’échange de messages avec IoT hub de hello.

Quand un appareil est connecté tooan IoT hub, le périphérique hello kits de développement logiciel fournissent des méthodes qui permettent de messages de toosend appareil hello tooand recevoir des messages à partir d’un hub IoT.

Hello tableau suivant contient des liens toocode exemples pour chaque langue prise en charge et spécifie hello paramètre toouse tooestablish un tooIoT connexion concentrateur à l’aide du protocole MQTT hello.

| language | Paramètre de protocole |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Migration d’une application de périphérique à partir de AMQP tooMQTT

Si vous utilisez hello [appareil kits de développement logiciel][lnk-device-sdks], passer de l’utilisation d’AMQP tooMQTT requiert la modification des paramètres de protocole hello dans l’initialisation du client hello comme indiqué précédemment.

Dans ce cas, assurez-vous que toocheck hello éléments suivants :

* AMQP retourne des erreurs pour nombreuses conditions, tandis que MQTT met fin à la connexion de hello. Par conséquent, votre logique de gestion des exceptions peut nécessiter certaines modifications.
* MQTT ne prend pas en charge hello *rejeter* opérations lors de la réception [messages cloud-à-appareil][lnk-messaging]. Si votre application back-end doit tooreceive une réponse à partir de l’application hello, envisagez d’utiliser [direct de méthodes][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>À l’aide de protocole MQTT hello directement
Si un appareil ne peut pas utiliser l’appareil hello kits de développement logiciel, il peut toujours se connecter les points de terminaison toohello périphérique public à l’aide du protocole MQTT hello sur le port 8883. Bonjour **CONNECT** dispositif de paquets hello doit utiliser hello valeurs suivantes :

* Pourquoi **ClientId** champ, utilisez hello **deviceId**.
* Pourquoi **nom d’utilisateur** champ, utilisez `{iothubhostname}/{device_id}/api-version=2016-11-14`, où {iothubhostname} est hello CName complète de hub IoT de hello.

    Par exemple, si hello nom de votre hub IoT est **contoso.azure-devices.net** et si le nom de votre appareil hello est **MyDevice01**, hello complète **nom d’utilisateur** champ doit contenir. `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Pourquoi **mot de passe** champ, utilisez un jeton SAP. format Hello Hello jeton SAP est même hello hello HTTP et les protocoles AMQP :<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Pour plus d’informations sur la façon toogenerate des jetons SAS, consultez la section de périphérique de hello de [des jetons de sécurité à l’aide de IoT Hub][lnk-sas-tokens].

    Lors du test, vous pouvez également utiliser hello [Explorateur de périphérique] [ lnk-device-explorer] tooquickly de l’outil génère un jeton SAP que vous pouvez copier et coller dans votre propre code :

  1. Accédez toohello **gestion** onglet **appareil Explorer**.
  2. Cliquez sur **SAS Token** (Jeton SAP) en haut à droite.
  3. Sur **SASTokenForm**, sélectionnez votre appareil dans hello **DeviceID** liste déroulante. Définissez votre **TTL**(Durée de vie).
  4. Cliquez sur **générer** toocreate votre jeton.

     Cette structure a Hello jeton SAS qui est généré : `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     Hello partie de ce jeton toouse comme hello **mot de passe** tooconnect de champ à l’aide de MQTT est : `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

Pour MQTT se connecter et se déconnecter de paquets, IoT Hub émet un événement sur hello **opérations analyse** canal avec des informations supplémentaires qui peuvent vous aider à tootroubleshoot des problèmes de connectivité.

### <a name="sending-device-to-cloud-messages"></a>Envoi de messages appareil-à-cloud

Après avoir établi une connexion réussie, un appareil peut envoyer à l’aide de messages tooIoT Hub `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` comme un **nom de la rubrique**. Hello `{property_bag}` élément permet de messages de toosend hello appareil avec des propriétés supplémentaires dans un format encodé en url. Par exemple :

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Cela `{property_bag}` élément utilise hello même encodage que pour les chaînes de requête dans le protocole de hello HTTP.
>
>

permet également d’application Hello `devices/{device_id}/messages/events/{property_bag}` comme hello **nom de la rubrique seront** toodefine *ne les messages* toobe transmis en tant qu’un message de télémétrie.

- IoT Hub ne prend pas en charge les messages QoS 2. Si une application de périphérique publie un message avec **QoS 2**, IoT Hub ferme la connexion de réseau hello.
- IoT Hub ne conserve pas les messages Retain. Si un périphérique envoie un message avec hello **conserver** indicateur défini too1, IoT Hub ajoute hello **x-opt-conserver** toohello message de la propriété application. Dans ce cas, au lieu de persistance hello conserver le message, le IoT Hub passe toohello principal application.
- IoT Hub ne prend en charge qu’une seule connexion MQTT active par appareil. Toute connexion MQTT pour le compte hello même ID de périphérique entraîne IoT Hub hello toodrop la connexion existante.

Pour en savoir plus, reportez-vous au [Guide du développeur de messages][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Réception de messages cloud-à-appareil

tooreceive des messages à partir de IoT Hub, un appareil doit s’abonner à l’aide de `devices/{device_id}/messages/devicebound/#` comme un **rubrique filtre**. Hello génériques multiniveaux  **#**  Bonjour filtre de rubrique est utilisée uniquement tooallow hello appareil tooreceive des propriétés supplémentaires dans le nom de la rubrique hello. IoT Hub n’autorise pas l’utilisation de hello Hello  **#**  ou **?** pour filtrer les sous-rubriques. IoT Hub n’étant pas un broker de messagerie pub-sub à usage général, il prend uniquement en charge les noms de rubrique hello documentée et les filtres de la rubrique.

Hello ne reçoit des messages à partir de IoT Hub, jusqu'à ce qu’il a ouvert le point de terminaison tooits spécifique au périphérique, représenté par hello `devices/{device_id}/messages/devicebound/#` filtre de rubrique. Une fois l’abonnement réussie a été établie, appareil de hello commence à recevoir des messages uniquement cloud-à-appareil qui ont été envoyés tooit tard hello d’abonnement de hello. Appareil de hello qui se connecte avec **CleanSession** indicateur défini trop**0**, abonnement de hello est conservée entre les différentes sessions. Dans ce cas, hello prochaine fois qu’il se connecte avec **CleanSession 0** périphérique de hello reçoit des messages en attente qui ont été envoyés tooit pendant qu’il a été déconnecté. Si le périphérique de hello utilise **CleanSession** indicateur défini trop**1** , il ne reçoit pas les messages à partir de IoT Hub jusqu'à ce qu’elle s’abonne tooits périphérique-point de terminaison.

IoT Hub remet les messages avec hello **nom de la rubrique** `devices/{device_id}/messages/devicebound/`, ou `devices/{device_id}/messages/devicebound/{property_bag}` s’il existe des propriétés de message. `{property_bag}` contient des paires clé/valeur codées URL de propriétés de message. Uniquement les propriétés de l’application et les propriétés système définissable par l’utilisateur (tel que **messageId** ou **correlationId**) sont inclus dans le jeu de propriétés hello. Les noms de propriété système ont le préfixe de hello  **$** , propriétés de l’application utilisent le nom de la propriété d’origine hello sans le préfixe.

Lorsqu’une application de périphérique s’abonne rubrique tooa avec **QoS 2**, IoT Hub accorde niveau QoS maximal 1 Bonjour **SUBACK** paquet. Après cela, IoT Hub remet appareil de toohello de messages à l’aide de la qualité de service 1.

### <a name="retrieving-a-device-twins-properties"></a>Récupération des propriétés d’un jumeau d’appareil

Tout d’abord, un appareil s’abonne trop`$iothub/twin/res/#`, les réponses de l’opération tooreceive hello. Ensuite, il envoie un message vide de tootopic `$iothub/twin/GET/?$rid={request id}`, avec une valeur par défaut pour **id de demande**. service de hello puis envoie un message de réponse contenant les données de double périphérique hello sur rubrique `$iothub/twin/res/{status}/?$rid={request id}`, à l’aide de hello même  **id de demande** en tant que requête de hello.

L’ID de la requête peut avoir n’importe quelle valeur valide de propriété de message, conformément au [Guide du développeur de messages IoT Hub][lnk-messaging], et l’état est validé comme entier.
les corps de réponse de Hello contient la section des propriétés de double de périphérique hello hello :

corps Hello hello identité entrée de Registre limitée toohello membre de « propriétés », par exemple :

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

Hello codes d’état possibles sont :

|État | Description |
| ----- | ----------- |
| 200 | Succès |
| 429 | Trop de demandes (limité), selon la [Limitation IoT Hub][lnk-quotas] |
| 5** | Erreurs de serveur |

Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Mettre à jour les propriétés signalées du jumeau d’appareil

Hello séquence suivante décrit comment un appareil met à jour hello a signalé des propriétés en double d’appareil hello dans IoT Hub :

1. Un appareil Abonnez-vous d’abord toohello `$iothub/twin/res/#` les réponses de l’opération de rubrique tooreceive hello du IoT Hub.

1. Un périphérique envoie un message qui contient hello appareil double mise à jour toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` rubrique. Ce message contient une valeur **ID de demande**.

1. Hello service puis envoie un message de réponse contenant hello nouvelle valeur d’ETag pour hello collection de propriétés déclarées sur la rubrique `$iothub/twin/res/{status}/?$rid={request id}`. Ce message de réponse utilise hello même **id de demande** en tant que requête de hello.

corps du message de demande de Hello contient un document JSON, qui fournit les nouvelles valeurs pour les propriétés déclarées (aucune autre propriété ou les métadonnées ne peuvent être modifiées).
Chaque membre dans le document JSON de hello met à jour ou ajouter des membres correspondants de hello dans les documents de double hello appareil. Un membre défini trop`null`, suppressions hello membre à partir de hello contenant l’objet. Par exemple :

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Hello codes d’état possibles sont :

|État | Description |
| ----- | ----------- |
| 200 | Succès |
| 400 | Demande incorrecte. JSON incorrect |
| 429 | Trop de demandes (limité), selon la [Limitation IoT Hub][lnk-quotas] |
| 5** | Erreurs de serveur |

Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Réception de notifications de mise à jour des propriétés souhaitées

Quand un appareil est connecté, IoT Hub envoie rubrique toohello de notifications `$iothub/twin/PATCH/properties/desired/?$version={new version}`, qui contiennent le contenu de mise à jour hello effectuée par hello solution back-end hello. Par exemple :

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Comme pour les mises à jour de la propriété, `null` signifie que les valeurs qui hello JSON est en cours de suppression des membres de l’objet.


> [!IMPORTANT] 
> IoT Hub génère des notifications de modification uniquement lorsque les appareils sont connectés. Assurez-vous que tooimplement hello [flux reconnexion de périphérique] [ lnk-devguide-twin-reconnection] tookeep hello souhaité propriétés synchronisées entre IoT Hub et application d’appareil hello.

Pour en savoir plus, reportez-vous au [Guide du développeur de jumeaux d’appareil][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Méthode directe de répondre tooa

Tout d’abord, un appareil a toosubscribe trop`$iothub/methods/POST/#`. IoT Hub envoie la rubrique de méthode demandes toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, avec un corps vide ou un JSON valid.

toorespond, appareil de hello envoie un message avec un JSON valid ou une rubrique de toohello de corps vide `$iothub/methods/res/{status}/?$rid={request id}`, où **id de demande** a toomatch un dans le message de demande hello, hello et **état** a toobe entier .

Pour en savoir plus, reportez-vous au [Guide du développeur de méthodes directes][lnk-methods].

### <a name="additional-considerations"></a>Considérations supplémentaires

En termes de finale, si vous avez besoin de comportement du protocole toocustomize hello MQTT côté hello cloud, vous devez passer en revue hello [passerelle de protocole Azure IoT] [ lnk-azure-protocol-gateway] qui vous permet de toodeploy hautes performances passerelle de protocole personnalisé qui interagit directement avec l’IoT Hub. passerelle de protocole Hello Azure IoT permet de vous toocustomize hello appareil protocole tooaccommodate brownfield MQTT déploiements ou autres protocoles personnalisés. Toutefois, cette approche nécessite l’exécution et l’utilisation d’une passerelle de protocole personnalisée.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur le protocole MQTT hello, consultez hello [documentation de MQTT][lnk-mqtt-docs].

toolearn savoir plus sur la planification de votre déploiement IoT Hub, consultez :

* [Catalogue d’appareils certifiés Azure pour l’IoT][lnk-devices]
* [Prendre en charge des protocoles supplémentaires][lnk-protocols]
* [Comparer à Event Hubs][lnk-compare]
* [Mise à l’échelle, HA et DR][lnk-scaling]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
