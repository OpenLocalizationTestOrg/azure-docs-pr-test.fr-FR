---
title: "aaaUnderstand Azure IoT Hub direct de méthodes | Documents Microsoft"
description: "Guide du développeur - utiliser le code tooinvoke méthodes directes sur vos appareils à partir d’une application de service."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Comprendre et appeler des méthodes directes à partir d’IoT Hub
## <a name="overview"></a>Vue d'ensemble
IoT Hub vous fournit des méthodes direct de capacité tooinvoke sur des périphériques de cloud de hello. Méthodes directes représentent une interaction de demande-réponse avec un tooan similaire de périphérique HTTP appeler dans la mesure où ils réussissent ou échouent immédiatement (après un délai d’attente spécifié par l’utilisateur). Cela est utile pour les scénarios où les cours hello d’action immédiate est différente selon si l’appareil de hello a été en mesure de toorespond, telles que l’envoi d’un périphérique de veille tooa SMS si un périphérique est hors connexion (SMS qui est plus onéreuse qu’un appel de méthode).

Chaque méthode d’appareil cible à un seul appareil. [Travaux] [ lnk-devguide-jobs] fournissent un tooinvoke moyen méthodes directes sur plusieurs appareils et planifier l’appel de méthode pour les appareils déconnectés.

Toute personne disposant d’autorisations **Connexion de service** sur IoT Hub peut appeler une méthode sur un appareil.

### <a name="when-toouse"></a>Lorsque toouse
Méthodes directes suivent un modèle de requête-réponse et sont destinés à des communications nécessitant une confirmation immédiate de leurs résultats, un contrôle généralement interactif d’appareil hello, par exemple tooturn sur un ventilateur.

Consultez trop[des conseils de communication Cloud-à-appareil] [ lnk-c2d-guidance] en cas de doute entre l’utilisation de propriétés souhaitées, diriger les méthodes ou les messages cloud-à-appareil.

## <a name="method-lifecycle"></a>Cycle de vie de méthode
Méthodes directes sont implémentés sur le périphérique de hello et peuvent nécessiter de zéro ou plusieurs entrées dans toocorrectly de charge utile de méthode hello instancier. Vous appelez une méthode directe via un URI côté service (`{iot hub}/twins/{device id}/methods/`). Un appareil reçoit des méthodes directes via une rubrique MQTT spécifique de l’appareil (`$iothub/methods/POST/{method name}/`). Nous pouvons prend en charge les méthodes directes sur les autres protocoles réseau côté appareil Bonjour futures.

> [!NOTE]
> Lorsque vous appelez une méthode directe sur un appareil, les valeurs et les noms de propriété ne peuvent contenir US-ASCII imprimable alphanumérique, à l’exception dans l’ensemble suivant de hello : ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Direct de méthodes synchrones, soit réussir ou échouer après le délai d’attente hello (valeur par défaut : 30 secondes, définissables des too3600 secondes). Méthodes directes sont utiles dans les scénarios interactifs où vous souhaitez un tooact périphérique si et seulement si le périphérique de hello est en ligne et de réception commandes, telles que l’activation une lumière à partir d’un téléphone. Dans ces scénarios, vous souhaitez toosee immédiate réussite ou l’échec pour que le service cloud hello puisse agir sur le résultat de hello dès que possible. Appareil de Hello peut retourner un corps de message en raison de la méthode hello, mais il n’est pas nécessaire pour hello méthode toodo donc. Il existe ni garantie de classement, ni sémantique de concurrence sur les appels de méthode.

Méthode directe sont HTTP uniquement du côté du cloud hello et MQTT uniquement du côté du périphérique hello.

charge utile de Hello pour les demandes de méthodes et des réponses est un document JSON de too8KB.

## <a name="reference-topics"></a>Rubriques de référence :
Hello rubriques de référence suivantes vous fournissent plus d’informations sur l’utilisation de méthodes directes.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Appeler une méthode directe à partir d’une application principale
### <a name="method-invocation"></a>Appel de méthode
Les appels de méthode directe sur un appareil sont des appels HTTP qui comprennent les éléments suivants :

* Hello *URI* toohello spécifique périphérique (`{iot hub}/twins/{device id}/methods/`)
* Hello POST *(méthode)*
* *En-têtes* qui contiennent hello authorization, de demander l’ID, type de contenu et le codage du contenu
* JSON transparent *corps* Bonjour suivant le format :

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

Le délai d’attente est exprimé en secondes. Si le délai d’attente n’est pas définie, la valeur par défaut too30 secondes.

### <a name="response"></a>Réponse
application de back-end Hello reçoit une réponse qui comprend :

* *Code d’état HTTP*, qui est utilisé pour les erreurs provenant de hello IoT Hub, y compris une erreur 404 pour les appareils pas actuellement connecté.
* *En-têtes* qui contiennent des hello ETag, de demander l’ID, type de contenu et le codage du contenu
* JSON *corps* Bonjour suivant le format :

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Les deux `status` et `body` sont fournies par le périphérique de hello et utilisées toorespond avec le code d’état du périphérique hello et/ou la description.

## <a name="handle-a-direct-method-on-a-device"></a>Gérer une méthode directe sur un appareil
### <a name="method-invocation"></a>Appel de méthode
Périphériques de recevoir des demandes de méthode directe sur la rubrique MQTT hello :`$iothub/methods/POST/{method name}/?$rid={request id}`

corps de Hello quel appareil hello reçoit est Bonjour suivant le format :

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Les demandes de méthode sont QoS 0.

### <a name="response"></a>Réponse
l’unité Hello envoie des réponses trop`$iothub/methods/res/{status}/?$rid={request id}`, où :

* Hello `status` propriété est l’état fourni par l’appareil de hello d’exécution de la méthode.
* Hello `$rid` propriété est hello demande à partir de l’appel de méthode hello provenant du IoT Hub.

corps de Hello est définie par l’appareil de hello et peut être n’importe quel état.

## <a name="additional-reference-material"></a>Matériel de référence supplémentaire
Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :

* [Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.
* [Limitation et les quotas] [ lnk-quotas] décrit les quotas hello qui s’appliquent toohello IoT Hub service hello limitation tooexpect de comportement lorsque vous utilisez le service de hello.
* [Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.
* [Langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages] [ lnk-query] décrit le langage de requête IoT Hub vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux de hello.
* [Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.

## <a name="next-steps"></a>Étapes suivantes
Maintenant, vous avez appris comment toouse des méthodes directes, vous pouvez être intéressé hello suivant rubrique du guide de développement IoT Hub :

* [Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]

Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant IoT Hub didacticiel :

* [Utiliser des méthodes directes][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
