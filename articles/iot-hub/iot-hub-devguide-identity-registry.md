---
title: "Registre des identités de Azure IoT Hub hello aaaUnderstand | Documents Microsoft"
description: "Guide du développeur - description de hello Registre des identités IoT Hub et la manière dont toouse il toomanage vos appareils. Inclut des informations sur l’importation de hello et l’exportation des identités de l’appareil en bloc."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>Comprendre le Registre des identités hello dans votre IoT hub

Chaque hub IoT a un registre des identités qui stocke des informations sur les périphériques hello autorisés tooconnect toohello IoT hub. Avant de connecter un appareil tooan IoT hub, il doit y avoir une entrée pour ce périphérique dans le Registre des identités de concentrateur hello IoT. Un appareil doit également s’authentifier avec hello IoT hub basé sur les informations d’identification stockées dans le Registre des identités hello.

ID de périphérique Hello stockée dans le Registre des identités hello respecte la casse.

À un niveau élevé, Registre des identités hello est une collection prenant en charge de REST identité de ressources de périphérique. Lorsque vous ajoutez une entrée dans le Registre des identités hello, IoT Hub crée un ensemble de ressources de chaque appareil comme file d’attente hello qui contient des messages cloud-à-appareil en cours.

### <a name="when-toouse"></a>Lorsque toouse

Utilisez le Registre des identités hello lorsque vous avez besoin :

* Configurer des appareils qui se connectent tooyour IoT hub.
* Contrôler les points de terminaison de périphérique du concentrateur de tooyour accès par périphérique.

> [!NOTE]
> Registre des identités Hello ne contient pas toutes les métadonnées spécifiques à l’application.

## <a name="identity-registry-operations"></a>Opérations du registre d’identité

Hello Registre des identités IoT Hub expose hello opérations suivantes :

* Création d’une identité d’appareil
* Mise à jour d’une identité d’appareil
* Récupération d’une identité d’appareil par ID
* Suppression d’une identité d’appareil
* Liste des identités de too1000
* Exporter le stockage d’objets blob tooAzure toutes les identités
* Importation de toutes les identités depuis le stockage Blob Azure

Toutes ces opérations peuvent utiliser un accès concurrentiel optimiste, comme spécifié dans [RFC7232][lnk-rfc7232].

> [!IMPORTANT]
> Hello tooretrieve de façon seulement toutes les identités dans le Registre des identités d’un hub IoT est toouse hello [exporter] [ lnk-export] fonctionnalité.

Un registre des identités IoT Hub :

* ne contient pas de métadonnées de l’application ;
* Est accessible comme un dictionnaire, à l’aide de hello **deviceId** en tant que clé de hello.
* ne prend pas en charge les requêtes expressives.

Une solution IoT possède généralement une zone de stockage distincte spécifique à la solution qui contient les métadonnées propres à l’application. Par exemple, hello magasin spécifique à la solution dans une solution de génération de smart doit enregistrer salle hello dans lequel un capteur de température est déployé.

> [!IMPORTANT]
> Utilisez uniquement Registre des identités hello pour la gestion des périphériques et opérations de configuration. Opérations de débit élevé au moment de l’exécution ne doivent pas dépendre de l’exécution d’opérations dans le Registre des identités hello. Par exemple, la vérification de l’état de connexion hello d’un appareil avant d’envoyer une commande n’est pas un modèle pris en charge. Assurez-vous que toocheck hello [taux de limitation] [ lnk-quotas] pour le Registre des identités hello et hello [pulsation de l’appareil] [ lnk-guidance-heartbeat] modèle.

## <a name="disable-devices"></a>Désactivation d’appareils

Vous pouvez désactiver les périphériques en mettant à jour hello **état** propriété d’une identité dans le Registre des identités hello. Généralement, cette propriété est utilisée dans deux scénarios :

* Au cours d’un processus d’orchestration d’approvisionnement. Pour plus d’informations, voir [Approvisionnement des appareils][lnk-guidance-provisioning].
* Si, pour une raison quelconque, vous pensez qu’un appareil est compromis ou non autorisé.

## <a name="import-and-export-device-identities"></a>Importer et exporter les identités des appareils

Vous pouvez exporter les identités des appareils en bloc à partir du Registre des identités d’un hub IoT, à l’aide des opérations asynchrones sur hello [point de terminaison IoT Hub ressource fournisseur][lnk-endpoints]. Les exportations sont longs travaux qui utilisent un données d’identité d’appareil fourni par le client de blob conteneur toosave lire à partir du Registre des identités hello.

Vous pouvez importer des identités d’appareil dans le Registre des identités du hub IoT en bloc tooan, à l’aide des opérations asynchrones sur hello [point de terminaison IoT Hub ressource fournisseur][lnk-endpoints]. Les importations sont des travaux à long terme qui utilisent des données dans un blob de fourni par le client conteneur toowrite appareil identité de données dans le Registre des identités hello.

* Pour obtenir des informations détaillées sur l’importation de hello et d’exportation des API, consultez [fournisseur de ressources IoT Hub API REST][lnk-resource-provider-apis].
* toolearn plus d’informations sur l’exécution importent et exporter les tâches, consultez [en bloc de gestion des identités des appareils IoT Hub][lnk-bulk-identity].

## <a name="device-provisioning"></a>Approvisionnement des appareils

données de l’appareil Hello contenant une solution IoT donnée dépendent hello spécifique de cette solution. Mais une solution doit au minimum stocker les clés d’authentification et les identités des appareils. Azure IoT Hub inclut un registre d’identité qui peut stocker des valeurs pour chaque appareil, comme les ID, les clés d’authentification et les codes d’état. Une solution peut utiliser des autres services Azure tels que le stockage de table, stockage d’objets blob ou Cosmos DB toostore toutes les données d’appareil supplémentaires.

*Configuration du périphérique* est hello des processus d’ajout de banques de toohello données hello initiale de l’appareil dans votre solution. tooenable un nouveau concentrateur de tooyour tooconnect de périphérique, vous devez ajouter un toohello ID et les clés appareil Registre des identités IoT Hub. Dans le cadre du processus d’approvisionnement de hello, vous devrez peut-être tooinitialize des données dans d’autres banques de la solution.

## <a name="device-heartbeat"></a>Pulsation des appareils

Registre des identités IoT Hub Hello contient un champ appelé **connectionState**. Utilisez uniquement hello **connectionState** champ pendant le développement et le débogage. IoT solutions doivent interroger pas de champ de hello en cours d’exécution. Par exemple, ne pas interroger hello **connectionState** toocheck champ si un appareil est connecté avant d’envoyer un message cloud-à-appareil ou un SMS.

Si votre solution IoT doit tooknow si un appareil est connecté, vous devez implémenter hello *modèle de pulsation*.

Dans le modèle de pulsation hello, appareil de hello envoie des messages de l’appareil-à-cloud au moins une fois chaque quantité fixe de temps (par exemple, au moins une fois par heure). Par conséquent, même si un appareil ne dispose pas de n’importe quel toosend de données, il envoie toujours un message vide de périphérique dans le cloud (généralement avec une propriété qui l’identifie comme une pulsation). Sur le côté du service hello, solution de hello gère un mappage avec hello dernière pulsation reçue pour chaque périphérique. Si la solution de hello ne reçoit pas d’un message de pulsation dans délai hello prévu à partir de l’appareil de hello, il part du principe qu’il existe un problème avec le périphérique de hello.

Une implémentation plus complexe peut inclure des informations de hello des [surveillance des opérations] [ lnk-devguide-opmon] périphériques tooidentify essaient tooconnect ou communiquent mais échouent. Lorsque vous implémentez le modèle de pulsation hello, assurez-vous que toocheck [IoT Hub Quotas et les accélérateurs][lnk-quotas].

> [!NOTE]
> Si une connexion de hello IoT solution utilise état toodetermine uniquement si les messages cloud-à-appareil toosend, et les messages ne sont pas toolarge des ensembles de périphériques de diffusion, envisagez d’utiliser le plus simple de hello *court délai d’expiration* modèle. Ce modèle permet d’obtenir hello même résultat que la gestion d’un Registre état de connexion de périphérique à l’aide du modèle de pulsation hello, tout en étant plus efficace. Si vous demandez les accusés de réception de message, IoT Hub peut vous informer sur les appareils qui sont en mesure de tooreceive messages et qui ne sont pas.

## <a name="device-lifecycle-notifications"></a>Notifications de cycle de vie des appareils

IoT Hub peut avertir votre solution IoT lorsqu’une identité d’appareil est créée ou supprimée, en envoyant des notifications de cycle de vie des appareils. toodo, votre solution IoT doit donc toocreate un itinéraire et égal de Source de données tooset hello trop*DeviceLifecycleEvents*. Par défaut, aucune notification du cycle de vie n’est envoyée. Autrement dit, aucun itinéraire n’existe préalablement. message de notification Hello inclut le corps et les propriétés.

Propriétés : Propriétés des messages système sont précédées hello `'$'` symbole.

| Nom | Valeur |
| --- | --- |
$content-type | application/json |
$iothub-enqueuedtime |  Heure à laquelle la notification de hello a été envoyée |
$iothub-message-source | deviceLifecycleEvents |
$content-encoding | utf-8 |
opType | **createDeviceIdentity** ou **deleteDeviceIdentity** |
hubName | Nom de l’IoT Hub |
deviceId | ID de périphérique de hello |
operationTimestamp | Horodatage ISO8601 de l’opération |
iothub-message-schema | deviceLifecycleNotification |

Corps : Cette section est au format JSON et représente le double de hello Hello créé l’identité de l’appareil. Par exemple,

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
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

## <a name="reference-topics"></a>Rubriques de référence :

Hello rubriques de référence suivantes vous fournissent plus d’informations sur le Registre des identités hello.

## <a name="device-identity-properties"></a>Propriétés d’identité des appareils

Identités de l’appareil sont représentées en tant que documents JSON par hello propriétés suivantes :

| Propriété | Options | Description |
| --- | --- | --- |
| deviceId |obligatoire, en lecture seule sur les mises à jour |Une chaîne qui respecte la casse (haut too128 caractères) de caractères ASCII 7 bits + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| generationId |obligatoire, en lecture seule |Une IoT respectant la casse, générées par le concentrateur, chaîne des caractères too128. Cette valeur est toodistinguish utilisé pour les appareils avec hello même **deviceId**, lorsqu’ils ont été supprimés et recréés. |
| etag |obligatoire, en lecture seule |Chaîne représentant un ETag faible pour l’identité de l’appareil hello, comme par [RFC7232][lnk-rfc7232]. |
| auth |facultatif |Un objet composite contenant des informations d’authentification et des éléments de sécurité. |
| auth.symkey |facultatif |Un objet composite contenant une clé primaire et une clé secondaire, stockées au format base64. |
| status |required |Un indicateur d’accès. Peut être **Activé** ou **Désactivé**. Si **activé**, hello est autorisé tooconnect. Si la propriété est définie sur **Désactivé**, cet appareil ne peut pas accéder à un point de terminaison de l’appareil. |
| statusReason |facultatif |Un 128 caractères de longueur de chaîne magasins hello raison hello appareil statut d’identité. Tous les caractères UTF-8 sont autorisés. |
| statusUpdateTime |en lecture seule |Un indicateur temporel, indiquant la date de hello et l’heure de mise à jour de statut dernière hello. |
| connectionState |en lecture seule |Un champ indiquant l’état de la connexion : **Connecté** ou **Déconnecté**. Ce champ représente hello vue IoT Hub du statut de connexion de périphérique hello. **Important**  : ce champ doit être utilisé uniquement à des fins de développement et de débogage. état de la connexion Hello est mise à jour uniquement pour les appareils à l’aide de MQTT ou AMQP. Cet état est basé sur les pings au niveau du protocole (tests ping MQTT ou AMQP) et peut avoir un délai maximum de 5 minutes seulement. Pour ces raisons, de faux positifs peuvent survenir. Par exemple : un appareil peut être signalé comme étant connecté, alors qu’il est déconnecté. |
| connectionStateUpdatedTime |en lecture seule |Un indicateur temporel, indiquant la date de hello et l’état de la connexion dernière heure hello a été mis à jour. |
| lastActivityTime |en lecture seule |Un indicateur temporel, indiquant la date de hello et dernière hello appareil connecté, reçu ou envoyé un message. |

> [!NOTE]
> État de la connexion peut représenter uniquement hello vue IoT Hub du statut hello de connexion de hello. État de toothis mises à jour peut être retardée, en fonction des configurations et des conditions réseau.

## <a name="additional-reference-material"></a>Matériel de référence supplémentaire

Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :

* [Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.
* [Limitation et les quotas] [ lnk-quotas] décrit les quotas hello et la limitation des comportements qui s’appliquent toohello IoT Hub service.
* [Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.
* [Langage de requête IoT Hub] [ lnk-query] décrit le langage de requête hello vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux.
* [Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.

## <a name="next-steps"></a>Étapes suivantes

Maintenant, vous avez appris comment Registre des identités toouse hello IoT Hub, vous pouvez être intéressé hello IoT Hub développeur guide rubriques suivantes :

* [Contrôle l’accès tooIoT Hub][lnk-devguide-security]
* [Utiliser les configurations et état du périphérique jumeaux toosynchronize][lnk-devguide-device-twins]
* [Appeler une méthode directe sur un appareil][lnk-devguide-directmethods]
* [Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]

Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant IoT Hub didacticiel :

* [Mise en route d’Azure IoT Hub][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
