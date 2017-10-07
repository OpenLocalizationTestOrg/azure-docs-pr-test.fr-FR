---
title: "aaaUnderstand Azure IoT Hub cloud-à-appareil messagerie | Documents Microsoft"
description: "Guide du développeur - comment toouse cloud-à-appareil messagerie avec IoT Hub. Inclut des informations sur le cycle de vie des messages hello et options de configuration."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>Envoyer des messages cloud-à-appareil à partir d’IoT Hub

application pour appareil toohello toosend des notifications à sens unique à partir de votre solution back-end, envoyer des messages de cloud aux appareils à partir de votre appareil tooyour de hub IoT. Pour une description des autres options cloud-à-appareil prises en charge par IoT Hub, consultez [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].

Vous envoyez les messages cloud-à-appareil via un point de terminaison côté service (**/messages/devicebound**). Un appareil reçoit ensuite les messages de type hello via un point de terminaison spécifique à l’appareil (**/devices/ {deviceId} / messages/devicebound**).

Chaque message cloud-à-appareil ciblée vers un seul périphérique en définissant un hello **à** propriété trop**/devices/ {deviceId} / messages/devicebound**.

Chaque file d’attente d’appareil peut contenir jusqu’à 50 messages cloud-à-appareil. La tentative de toosend plusieurs messages toohello même appareil génère une erreur.

## <a name="hello-cloud-to-device-message-lifecycle"></a>cycle de vie des cloud-à-appareil message Hello

tooguarantee au moins une remise de messages IoT Hub persiste messages cloud-à-appareil dans les files d’attente par périphérique. Les appareils doivent accepter explicitement *achèvement* pour IoT Hub tooremove de hello file d’attente. Cette approche garantit la résilience contre les échecs de connectivité et d’appareils.

Hello diagramme suivant montre graphique d’état hello du cycle de vie d’un message cloud-à-appareil dans IoT Hub.

![Cycle de vie des messages cloud-à-appareil][img-lifecycle]

Lorsque hello IoT Hub service envoie un dispositif de tooa de message, le service de hello définit un état de message hello trop**empilés**. Lorsqu’un appareil veut trop*réception* un message, IoT Hub *verrous* message de type hello (en plaçant hello trop**Invisible**), ce qui autorise les autres threads sur hello appareil toostart recevoir d’autres messages. Un thread de l’appareil après traitement hello d’un message, il avertit IoT Hub par *fin* message de type hello. IoT Hub attribue ensuite à hello état trop**terminé**.

Un appareil peut également choisir de :

* *Rejeter* message de type hello, ce qui entraîne l’IoT Hub tooset il toohello **inactivé** état. Appareils qui se connectent via le protocole MQTT de hello ne peut pas refuser des messages cloud-à-appareil.
* *Abandonner* message de type hello, ce qui entraîne des message de type hello tooput IoT Hub en file d’attente de hello, avec l’état hello défini trop**empilés**.

Un thread peut échouer tooprocess un message sans en avertir l’IoT Hub. Dans ce cas, automatiquement des messages transition de hello **Invisible** toohello retour d’état **empilés** état après un *délai d’attente de visibilité (ou un verrou)*. Hello par défaut de ce délai d’attente est une minute.

Un message peut effectuer la transition entre hello **empilés** et **Invisible** États, hello au maximum, le nombre de fois spécifié dans hello **max de diffusions** propriété IoT Hub. Une fois ce nombre de transitions, IoT Hub définit état hello de message de type hello trop**inactivé**. De même, IoT Hub définit état hello d’un message trop**inactivé** après son heure d’expiration (voir [temps toolive][lnk-ttl]).

Hello [comment les messages toosend cloud-à-appareil avec IoT Hub] [ lnk-c2d-tutorial] vous montre comment les messages cloud-à-appareil toosend de hello de cloud computing et les recevoir sur un appareil.

En règle générale, un périphérique termine un message cloud-à-appareil lors de la perte de hello de message de type hello n’affecte pas la logique d’application hello. Par exemple, lorsque hello périphérique a rendu persistant contenu du message hello localement ou a exécuté avec succès d’une opération. message de type Hello pourrait exécuter également des informations temporaires, dont la perte n’aurait aucun impact sur les fonctionnalités de hello d’application hello. Dans certains cas, pour les tâches longues, vous pouvez terminer message cloud-à-appareil de type hello après la persistance hello description de la tâche dans le stockage local. Ensuite, vous pouvez notifier hello solution principal avec un ou plusieurs messages appareil-à-cloud à différents niveaux de progression de la tâche hello.

## <a name="message-expiration-time-toolive"></a>Expiration du message (heure toolive)

Chaque message cloud-à-appareil est doté d’un délai d’expiration. Cette heure est définie par le service de hello (Bonjour **ExpiryTimeUtc** propriété), ou par IoT Hub à l’aide de la valeur par défaut hello *temps toolive* spécifié comme propriété IoT Hub. Consultez [Options de configuration cloud-à-appareil][lnk-c2d-configuration].

Un avantage tootake moyen commun d’expiration du message et éviter d’envoyer des messages toodisconnected périphériques, est tooset valeurs toolive d’heure courte. Cette approche permet d’obtenir hello même résultat que la gestion de l’état de connexion de périphérique hello, tout en étant plus efficace. Lorsque vous demandez les accusés de réception de message, IoT Hub vous signale les appareils qui sont en mesure de tooreceive messages, et les appareils qui ne sont pas en ligne ou ont échoué.

## <a name="message-feedback"></a>Commentaires de messages

Lorsque vous envoyez un message cloud-à-appareil, service de hello peut demander la remise de hello de commentaires par message concernant l’état final de hello de ce message.

| Propriété Ack | Comportement |
| ------------ | -------- |
| **positive** | IoT Hub génère un message de commentaires si et uniquement si message cloud-à-appareil de type hello atteint hello **terminé** état. |
| **negative** | IoT Hub génère un message de commentaires si et seulement si, message cloud-à-appareil de type hello atteint hello **inactivé** état. |
| **full**     | IoT Hub génère un message de commentaires dans les deux cas. |

Si **l’accusé de réception** est **complète**et vous ne recevez pas un message d’évaluation, cela signifie que hello commentaires est arrivé à expiration. Bonjour service ne peut pas savoir quel message d’origine toohello s’est produit. Dans la pratique, un service doit s’assurer qu’il peut traiter les commentaires de hello avant son expiration. délai d’expiration maximal de Hello est de deux jours, ce qui permet de beaucoup de temps tooget hello service en cours d’exécution à nouveau si une défaillance se produit.

Comme l’explique la section [Points de terminaison][lnk-endpoints], IoT Hub fournit des commentaires sous la forme de messages par le biais d’un point de terminaison accessible au service (**/messages/servicebound/feedback**). Hello sémantique pour recevoir des commentaires sont hello même que pour les messages cloud-à-appareil et avoir hello même [cycle de vie du Message][lnk-lifecycle]. Dès que possible, des commentaires de message sont groupés dans un seul message, avec hello suivant le format :

| Propriété     | Description |
| ------------ | ----------- |
| EnqueuedTime | Horodatage indiquant quand le message de type hello a été créé. |
| UserId       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

corps de Hello est un tableau sérialisé en JSON d’enregistrements, chacun avec hello propriétés suivantes :

| Propriété           | Description |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | Horodatage indiquant quand le résultat hello de message de type hello s’est produite. Par exemple, hello périphérique s’est terminée ou hello est arrivé à expiration. |
| OriginalMessageId  | **MessageId** de hello cloud-à-appareil message toowhich ces informations de commentaires est lié. |
| StatusCode         | Chaîne obligatoire. Utilisé dans les messages de commentaires générés par IoT Hub. <br/> « Succès » <br/> « Expiré » <br/> « DeliveryCountExceeded »  <br/> « Rejeté » <br/> « Vidé » |
| Description        | Valeurs de chaîne pour **StatusCode**. |
| deviceId           | **DeviceId** du périphérique cible hello hello cloud-à-appareil message toowhich cet élément de commentaires est lié. |
| DeviceGenerationId | **DeviceGenerationId** du périphérique cible hello hello cloud-à-appareil message toowhich cet élément de commentaires est lié. |

service de Hello doit spécifier un **MessageId** pour hello cloud-à-appareil message toocorrelate en mesure de toobe ses commentaires avec le message d’appel d’origine.

Hello suivant montre les corps de hello d’un message de commentaires.

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>Options de configuration cloud-à-appareil

Chaque hub IoT expose hello des options de configuration pour la messagerie cloud-à-appareil suivantes :

| Propriété                  | Description | Plage et valeur par défaut |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | Durée de vie par défaut pour les messages cloud-à-appareil. | Intervalle de ISO_8601 des too2D (au minimum 1 minute). Par défaut : 1 heure. |
| maxDeliveryCount          | Nombre de remises maximal pour les files d’attente par appareil cloud-à-appareil | 1 too100. Par défaut : 10. |
| feedback.ttlAsIso8601     | Rétention des messages de commentaires liés au service. | Intervalle de ISO_8601 des too2D (au minimum 1 minute). Par défaut : 1 heure. |
| feedback.maxDeliveryCount |Nombre de remises maximal pour la file d’attente de commentaires. | 1 too100. Par défaut : 100. |

Pour plus d’informations sur comment tooset ces options de configuration, consultez [créer des IoT hubs][lnk-portal].

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les kits de développement logiciel hello, vous pouvez utiliser les messages cloud-à-appareil tooreceive, consultez [kits de développement logiciel Azure IoT][lnk-sdks].

tootry à recevoir des messages de cloud sur l’appareil, consultez hello [envoyer cloud-à-appareil] [ lnk-c2d-tutorial] didacticiel.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
