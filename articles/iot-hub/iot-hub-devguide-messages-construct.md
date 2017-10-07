---
title: format du message Azure IoT Hub aaaUnderstand | Documents Microsoft
description: "Guide du développeur - format de hello décrit et contenu attendu de messages de IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Créer et lire des messages IoT Hub

toosupport une interopérabilité transparente entre les protocoles, IoT Hub définit un format identique pour tous les protocoles de périphérique. Ce format est utilisé pour les messages [appareil-à-cloud][lnk-d2c] et [cloud-à-appareil][lnk-c2d]. Un [message IoT Hub][lnk-messaging] comprend les éléments suivants :

* Un ensemble de *propriétés système*. Propriétés interprétées ou définies par IoT Hub. Cet ensemble est prédéterminé.
* Un ensemble de *propriétés de l’application*. Dictionnaire de propriétés de chaîne hello application peut définir et d’accès, sans avoir besoin de corps du message toodeserialize hello. IoT Hub ne modifie jamais ces propriétés.
* Un corps binaire opaque.

Les valeurs et les noms de propriétés peuvent contenir uniquement des caractères alphanumériques ASCII, plus les caractères ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}``, quand vous effectuez les opérations suivantes :

* Envoyer des messages appareil-à-cloud à l’aide du protocole HTTP de hello.
* Envoyer des messages cloud-à-appareil.

Pour plus d’informations sur la façon tooencode et décoder les messages envoyés à l’aide de différents protocoles, consultez [kits de développement logiciel Azure IoT][lnk-sdks].

Hello tableau suivant répertorie hello de propriétés système dans les messages d’IoT Hub.

| Propriété | Description |
| --- | --- |
| MessageId |Un identificateur définissable par l’utilisateur pour le message de salutation utilisé pour les modèles de demande-réponse. Format : Un chaînes respectant la casse (haut too128 caractères) de caractères ASCII 7 bits + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Numéro de séquence |Nombre (unique pour chaque file d’attente de périphérique) affecté par IoT Hub tooeach cloud-à-appareil de message. |
| trop|Une destination spécifiée dans les messages [cloud-à-appareil][lnk-c2d]. |
| ExpiryTimeUtc |Date et heure d’expiration du message. |
| EnqueuedTime |Date et heure hello [Cloud-à-appareil] [ lnk-c2d] message a été reçu par IoT Hub. |
| CorrelationId |Propriété de chaîne dans un message de réponse qui contient généralement hello ID du message de demande de hello, dans les modèles de demande-réponse. |
| UserId |Un ID utilisé origine hello de toospecify de messages. Lorsque des messages sont générés par IoT Hub, il est défini trop`{iot hub name}`. |
| Ack |Un générateur de messages de commentaires. Cette propriété est utilisée dans les messages de commentaires messages cloud-à-appareil toorequest IoT Hub toogenerate à la suite de la consommation de message de type hello hello par périphérique de hello. Les valeurs possibles : **aucun** (par défaut) : aucun message de commentaires est généré, **positif**: recevoir un message de commentaires si le message de salutation a été effectué, **négatif**: recevoir un message d’évaluation si hello est arrivé à expiration (ou nombre maximal de diffusions a été atteint) sans réalisée par périphérique hello ou **complète**: positives et négatives. Pour plus d’informations, consultez [Commentaires sur les messages][lnk-feedback]. |
| ConnectionDeviceId |Un ID défini par IoT Hub sur les messages appareil vers cloud. Il contient hello **deviceId** du périphérique hello qui a envoyé le message de type hello. |
| ConnectionDeviceGenerationId |Un ID défini par IoT Hub sur les messages appareil vers cloud. Il contient hello **ID de génération** (comme par [propriétés d’identité appareil][lnk-device-properties]) du périphérique hello qui a envoyé le message de type hello. |
| ConnectionAuthMethod |Une méthode d’authentification définie par IoT Hub sur les messages appareil-à-cloud. Cette propriété contient des informations sur le périphérique hello hello d’authentification méthode utilisée tooauthenticate envoi de message de type hello. Pour plus d’informations, consultez [périphérique toocloud anti-usurpation][lnk-antispoofing]. |

## <a name="message-size"></a>Taille des messages

IoT Hub mesure la taille du message de manière agnostique du protocole, vous envisagez uniquement charge utile réelle de hello. taille en octets de Hello est calculé en tant que somme hello suivants de hello :

* taille du corps Hello en octets.
* taille de Hello en octets de toutes les valeurs hello hello système de propriétés de message.
* taille de Hello en octets de tous les noms de propriété d’utilisateur et de valeurs.

Les noms de propriété et les valeurs étant limité tooASCII caractères, la longueur des chaînes de hello hello est égal à la taille de hello en octets.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les limites de taille des messages dans IoT Hub, consultez [Quotas et limitation IoT Hub][lnk-quotas].

toolearn toocreate et lecture de messages IoT Hub dans différents langages de programmation, voir hello [prise en main] [ lnk-get-started] didacticiels.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
