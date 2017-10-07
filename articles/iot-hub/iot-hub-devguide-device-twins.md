---
title: "jumeaux de périphérique Azure IoT Hub aaaUnderstand | Documents Microsoft"
description: "Guide du développeur - utiliser le périphérique jumeaux toosynchronize les données de configuration et d’état entre IoT Hub et vos périphériques"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>Comprendre et utiliser les jumeaux d’appareil IoT Hub
## <a name="overview"></a>Vue d'ensemble
Les *jumeaux d’appareil* sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions). IoT Hub conserve un double du périphérique pour chaque périphérique que vous vous connectez tooIoT Hub. Cet article explique :

* Hello structure de double de périphérique hello : *balises*, *souhaitée* et *signalé propriétés*, et
* opérations de Hello que les applications de périphérique et back-end peut effectuer sur jumeaux de périphérique.

> [!NOTE]
> Actuellement, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello. Consultez toohello [prise en charge MQTT] [ lnk-devguide-mqtt] article pour obtenir des instructions sur la façon de tooconvert existant appareil application toouse MQTT.
> 
> 

### <a name="when-toouse"></a>Lorsque toouse
Vous pouvez utiliser des représentations d’appareil pour répondre aux besoins suivants :

* Stocker les métadonnées spécifiques au périphérique dans le cloud de hello. Par exemple, hello emplacement de déploiement d’un distributeur automatique.
* Signaler les informations d’état actuel, telles que les capacités disponibles et les conditions, à partir de votre application pour appareil, Par exemple, un périphérique est connecté tooyour IoT hub over cellulaire ou Wi-Fi.
* Synchroniser l’état hello de flux de travail de longue entre l’application et d’applications principal. Par exemple, lors de la solution de hello fin spécifie hello nouvelle tooinstall de version du microprogramme et les rapports application hello périphériques hello différentes étapes du processus de mise à jour hello.
* Interroger les métadonnées, la configuration ou l’état de vos appareils

Consultez trop[des conseils de communication de périphérique dans le cloud] [ lnk-d2c-guidance] pour obtenir des conseils sur l’utilisation de propriétés signalées, messages appareil-à-cloud ou téléchargement du fichier.
Consultez trop[des conseils de communication Cloud-à-appareil] [ lnk-c2d-guidance] pour obtenir des conseils sur l’utilisation de propriétés souhaitées, des méthodes directes ou des messages cloud-à-appareil.

## <a name="device-twins"></a>Jumeaux d’appareil
Les jumeaux d’appareil stockent des informations relatives aux appareils, dont l’utilité est la suivante :

* Se termine, puis dans l’appareil peut utiliser configuration et les conditions de périphérique toosynchronize.
* Hello solution back-end tooquery et de cibler les opérations longues.

Hello de cycle de vie d’un double de l’appareil est lié toohello correspondant [identité d’appareil][lnk-identity]. Des jumeaux d’appareil sont implicitement créés et supprimés lors de la création ou de la suppression d’une identité d’appareil dans IoT Hub.

Un jumeau d’appareil est un document JSON incluant les éléments suivants :

* **Tags** (balises). Une section du document JSON hello hello back-end solution peut lire et écrire dans. Les balises ne sont pas visibles toodevice applications.
* **Propriétés souhaitées (Desired)**. Utilisé avec la configuration de l’appareil toosynchronize propriétés déclarées ou conditions. Propriétés souhaitées ne peuvent être définies par la solution hello précédent fin et peuvent être lues par l’application hello. application Hello peut également être notifiée en temps réel des modifications dans les propriétés de hello souhaité.
* **Propriétés signalées (Reported)**. Utilisée avec la configuration de l’appareil toosynchronize propriétés souhaitées ou de conditions. Les propriétés déclarées ne peut être définies par l’application d’appareil hello et pouvant être lus et interrogées par hello solution back-end.

En outre, racine hello du document JSON de hello appareil double contient les propriétés d’en lecture seule de hello d’identité appareil correspondant de hello stockées dans hello [Registre des identités][lnk-identity].

![][img-twin]

Hello, l’exemple suivant montre un document JSON de double appareil :

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

Dans l’objet racine de hello, est des propriétés système hello et conteneur des objets pour `tags` et `reported` et `desired` propriétés. Hello `properties` conteneur contient des éléments en lecture seule (`$metadata`, `$etag`, et `$version`) décrit dans hello [appareil double métadonnées] [ lnk-twin-metadata] et [ L’accès concurrentiel optimiste] [ lnk-concurrency] sections.

### <a name="reported-property-example"></a>Exemple de propriété signalée (Reported)
Dans l’exemple précédent de hello, double du périphérique hello contient un `batteryLevel` propriété qui est signalée par l’application d’appareil hello. Cette propriété rend possible tooquery et opérer sur les périphériques en fonction du niveau de batterie signalé dernier hello. Autres exemples incluent des fonctions de rapport appareil hello appareil app ou des options de connectivité.

> [!NOTE]
> Les propriétés déclarées simplifient les scénarios où hello solution back-end est intéressé par hello dernière connue de valeur d’une propriété. Utilisez [messages appareil-à-cloud] [ lnk-d2c] si hello solution back-end a besoin de télémétrie de l’appareil tooprocess sous forme de hello de séquences d’événements horodaté, telles que de série chronologique.

### <a name="desired-property-example"></a>Exemple de propriété souhaitée
Dans l’exemple précédent de hello, hello `telemetryConfig` double de l’appareil souhaité et propriétés déclarées sont utilisées par hello solution back-end hello configuration et appareils application toosynchronize hello télémétrie pour cet appareil. Par exemple :

1. Hello solution back-end définit la propriété hello souhaitée avec la valeur de configuration hello souhaité. Voici la partie hello du document hello avec le jeu de propriétés hello souhaité :
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. application d’appareil Hello est avertie de modification hello immédiatement si connecté, ou à hello tout d’abord vous reconnecter. Hello application puis signale hello mise à jour de configuration (ou une condition d’erreur à l’aide de hello `status` propriété). Voici partie hello Hello signalé propriétés :
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. Hello solution back-end peut effectuer le suivi des résultats de l’opération de configuration hello hello sur plusieurs périphériques, par [interrogation] [ lnk-query] jumeaux de périphérique.

> [!NOTE]
> Hello des extraits de code précédents sont des exemples, optimisé pour une meilleure lisibilité, d’une façon tooencode une configuration de l’appareil et son état. IoT Hub n’impose pas un schéma spécifique pour double du périphérique hello souhaitée et a signalé des propriétés dans jumeaux de périphérique hello.
> 
> 

Vous pouvez utiliser jumeaux toosynchronize opérations longues telles que des mises à jour du microprogramme. Pour plus d’informations sur comment toouse propriétés toosynchronize et suivre une opération longue pour les appareils, consultez [utilisation souhaitée propriétés tooconfigure dispositifs][lnk-twin-properties].

## <a name="back-end-operations"></a>Opérations principales
Hello solution back-end fonctionne sur le double de périphérique hello à l’aide de hello suivant des opérations atomiques, exposées via le protocole HTTP :

1. **Récupérer la représentation d’appareil par son id**. Cette opération renvoie le document de double hello périphérique, y compris les balises et que vous le souhaitez, est signalé et les propriétés système.
2. **Mettre à jour partiellement le jumeau d’appareil**. Cette opération permet de balises de hello hello solution back-end toopartially mise à jour les propriétés souhaitées dans un double de l’appareil. mise à jour partielle de Hello est exprimée sous forme de document JSON qui ajoute ou met à jour n’importe quelle propriété. Propriétés définies trop`null` sont supprimés. Hello exemple suivant crée une nouvelle propriété souhaitée avec la valeur `{"newProperty": "newValue"}`, remplace la valeur existante de hello de `existingProperty` avec `"otherNewValue"`et supprime `otherOldProperty`. Aucuns autres modifications ne sont apportées tooexisting souhaité propriétés ou les balises :
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **Remplacer des propriétés souhaitées**. Cette toocompletely back-end de solution opération active hello remplacer toutes les propriétés de votre choisies et la remplacer par un nouveau document JSON pour `properties/desired`.
4. **Remplacer des Tags**. Cette toocompletely back-end de solution opération active hello remplacer toutes les balises existantes et les remplacer par un nouveau document JSON pour `tags`.
5. **Recevoir des notifications jumelles**. Cette opération permet de hello solution back-end toobe informé double de hello est modifiée. toodo, votre solution IoT doit donc toocreate un itinéraire et égal de Source de données tooset hello trop*twinChangeEvents*. Par défaut, aucune notification jumelle n’est envoyée. Autrement dit, aucun itinéraire n’existe préalablement. Si hello des taux de modification est trop élevé, ou pour d’autres raisons, telles que des défaillances internes, hello IoT Hub peut envoyer une notification qu’une seule qui contient toutes les modifications. Par conséquent, si l’audit et la journalisation fiables de tous les états intermédiaires sont nécessaires pour votre application, il est toujours recommandé d’utiliser les messages D2C. message de notification de double Hello inclut le corps et les propriétés.

    - Propriétés

    | Name | Valeur |
    | --- | --- |
    $content-type | application/json |
    $iothub-enqueuedtime |  Heure à laquelle la notification de hello a été envoyée |
    $iothub-message-source | twinChangeEvents |
    $content-encoding | utf-8 |
    deviceId | ID de périphérique de hello |
    hubName | Nom de l’IoT Hub |
    operationTimestamp | Horodatage [ISO8601] de l’opération |
    iothub-message-schema | deviceLifecycleNotification |
    opType | « replaceTwin » ou « updateTwin » |

    Propriétés des messages système sont précédées de hello `'$'` symbole.

    - Corps
        
    Cette section inclut toutes les modifications de double hello dans un format JSON. Elle utilise hello même format comme un correctif, avec différence de hello qu’elle peut contenir toutes les sections de double : balises, properties.reported, properties.desired et qu’il contient des éléments de hello « $metadata ». Par exemple,
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

Tous les hello prise en charge des opérations précédentes [d’accès concurrentiel optimiste] [ lnk-concurrency] et nécessitent hello **ServiceConnect** autorisation, tel que défini dans hello [sécurité ] [ lnk-security] l’article.

En outre les opérations toothese, solution de hello sauvegarder fin peut :

* Requête jumeaux de périphérique hello à l’aide de hello type SQL [langage de requête IoT Hub][lnk-query].
* Effectuer des opérations sur les grands ensembles de jumeaux d’appareil à l’aide de [travaux][lnk-jobs].

## <a name="device-operations"></a>Opérations d’appareil
application d’appareil Hello opère sur double d’appareil hello à l’aide de hello suivant des opérations atomiques :

1. **Récupérer le jumeau d’appareil**. Cette opération retourne le document de double hello appareil (y compris les balises et vous le souhaitez, signalée et les propriétés système) pour hello connecté actuellement le périphérique.
2. **Mettre à jour partiellement les propriétés signalées (Reported)**. Cette opération active hello mise à jour partielle de hello a signalé des propriétés d’appareil actuellement connectée de hello. Cette hello d’utilise opération JSON même mettre à jour de format qui utilise retour de fin hello solution pour une mise à jour partielle de propriétés souhaitées.
3. **Observer les propriétés souhaitées (Desired)**. la possibilité de toobe averti des propriétés toohello souhaité de mises à jour lorsqu’elles surviennent, Hello un périphérique actuellement connecté. Hello reçoit hello même formulaire de mise à jour (remplacement partiel ou complet) exécutée par hello solution back-end.

Tous les hello opérations précédentes nécessitent hello **DeviceConnect** autorisation, tel que défini dans hello [sécurité] [ lnk-security] l’article.

Hello [Azure IoT appareil kits de développement logiciel] [ lnk-sdks] rendre hello toouse facile à partir de nombreuses langues et plateformes, les opérations précédentes. Vous trouverez plus d’informations sur les détails de hello de primitives IoT Hub pour la synchronisation de propriétés souhaitées dans [flux reconnexion de périphérique][lnk-reconnection].

> [!NOTE]
> Actuellement, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello.
> 
> 

## <a name="reference-topics"></a>Rubriques de référence :
Hello rubriques de référence suivantes vous fournissent plus d’informations sur tooyour IoT hub de contrôler l’accès.

## <a name="tags-and-properties-format"></a>Format des Tags et propriétés
Balises, les propriétés souhaitées et signalées sont des objets JSON avec hello suivant restrictions :

* Toutes les clés dans des objets JSON sont des chaînes UNICODE UTF-8 de 64 octets respectant la casse. Les caractères autorisés excluent les caractères de contrôle UNICODE (segments C0 et C1), ainsi que `'.'`, `' '` et `'$'`.
* Toutes les valeurs dans des objets JSON peuvent être de hello JSON types suivants : booléen, nombre, chaîne, objet. Les tableaux ne sont pas autorisés.
* Tous les objets JSON dans les balises ainsi que dans les propriétés souhaitées et signalées, peuvent avoir une profondeur maximale de 5. Par exemple, hello objet est valide :

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* Aucune valeur de chaîne ne peut avoir une longueur supérieure à 512 octets.

## <a name="device-twin-size"></a>Taille de jumeau d’appareil
IoT Hub impose une limite de taille de 8 Ko sur les valeurs hello de `tags`, `properties/desired`, et `properties/reported`, à l’exclusion des éléments en lecture seule.
Hello taille est calculée en comptant tous les caractères UNICODE contrôlent caractères (segments C0 et C1) et l’espace `' '` lorsqu’il apparaît en dehors d’une constante de chaîne.
IoT Hub rejette, avec une erreur, toutes les opérations qui augmentent taille hello de ces documents dépasse la limite de hello.

## <a name="device-twin-metadata"></a>Métadonnées de jumeau d’appareil
IoT Hub conserve timestamp hello de hello dernière mise à jour pour chaque objet JSON en double de l’appareil souhaité et qu’il a signalé des propriétés. Hello horodatages sont au format UTC et encodé dans hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.
Par exemple :

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Ces informations sont conservées à chaque niveau (feuilles hello pas simplement de hello structure JSON) toopreserve mises à jour de supprimer des clés de l’objet.

## <a name="optimistic-concurrency"></a>Accès concurrentiel optimiste
Les Tags ainsi que les propriétés souhaitées (Desired) et signalées (Reported) prennent en charge l’accès concurrentiel optimiste.
Balises ont un ETag, comme par [RFC7232], qui représente la représentation JSON de la balise hello. Vous pouvez utiliser les ETags dans les opérations de mise à jour conditionnelle à partir de la cohérence de tooensure hello solution back-end.

Double du périphérique souhaité et signalés propriétés ETag est inutile, mais ont un `$version` valeur est garantie toobe incrémentielle. Même tooan ETag, version de hello peut être utilisée par hello mise à jour de la cohérence de tooenforce tiers des mises à jour. Par exemple, une application de périphérique pour signalé propriété ou hello solution principale pour une propriété de votre choix.

Les versions sont également utiles lorsqu’un agent observation (par exemple, application de périphérique hello en observant les propriétés hello souhaité) devez rapprocher courses entre le résultat de hello d’une opération de récupération et une notification de mise à jour. Hello section [flux reconnexion de périphérique] [ lnk-reconnection] fournit plus d’informations.

## <a name="device-reconnection-flow"></a>Flux de reconnexion d’appareil
IoT Hub ne conserve pas les notifications de mise à jour de propriétés souhaitées pour les appareils déconnectés. Il en résulte qu’un périphérique qui se connecte doit récupérer hello complète souhaitée document des propriétés, dans toosubscribing d’addition pour les notifications de mise à jour. Étant donné le risque de hello de courses entre les notifications de mise à jour et de récupération complète, hello suit flux doit être assurée :

1. Application de l’appareil connecte tooan IoT hub.
2. L’application d’appareil s’abonne aux notifications de mise à jour des propriétés souhaitées.
3. Application d’appareil récupère hello complète pour le document pour les propriétés souhaitées.

application d’appareil Hello peut ignorer toutes les notifications avec `$version` inférieure ou égale à la version de hello de hello complète récupérées pour le document. Cette approche est possible, car IoT Hub garantit que les numéros de version sont toujours incrémentiels.

> [!NOTE]
> Cette logique est déjà implémentée dans hello [Azure IoT appareil kits de développement logiciel][lnk-sdks]. Cette description est utile uniquement si l’application hello ne peut pas utiliser une de l’appareil Azure IoT kits de développement logiciel et devez programmer interface MQTT de hello directement.
> 
> 

## <a name="additional-reference-material"></a>Matériel de référence supplémentaire
Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :

* Hello [points de terminaison IoT Hub] [ lnk-endpoints] hello décrit les différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.
* Hello [limitation et les quotas] [ lnk-quotas] décrit les quotas hello qui s’appliquent toohello IoT Hub service hello limitation tooexpect de comportement lorsque vous utilisez le service de hello.
* Hello [SDK de périphérique et le service Azure IoT] [ lnk-sdks] article listes hello différents langage SDK, vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.
* Hello [langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages] [ lnk-query] décrit le langage de requête IoT Hub vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux de hello .
* Hello [prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] article fournit plus d’informations sur la prise en charge de IoT Hub pour le protocole MQTT hello.

## <a name="next-steps"></a>Étapes suivantes
Maintenant vous avez permis de découvrir jumeaux de périphérique, peut vous intéresser hello IoT Hub développeur guide rubriques suivantes :

* [Appeler une méthode directe sur un appareil][lnk-methods]
* [Planifier des travaux sur plusieurs appareils][lnk-jobs]

Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant les didacticiels IoT Hub :

* [Comment toouse hello double de l’appareil][lnk-twin-tutorial]
* [Comment toouse appareil à deux propriétés][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
