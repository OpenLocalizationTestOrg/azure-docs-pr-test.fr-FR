---
title: "téléchargement du fichier Azure IoT Hub aaaUnderstand | Documents Microsoft"
description: "Guide du développeur - fonctionnalité de téléchargement du fichier utilisation hello de toomanage IoT Hub téléchargement de fichiers à partir d’un conteneur d’objets blob Azure storage appareil tooan."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a>Chargement de fichiers avec IoT Hub

Comme détaillé dans hello [points de terminaison IoT Hub] [ lnk-endpoints] article, un périphérique peut initier le chargement d’un fichier en envoyant une notification via un point de terminaison du périphérique (**/devices/ {deviceId} / fichiers**). Lorsqu’un appareil avertit IoT Hub qu’un téléchargement est terminé, IoT Hub envoie un message de notification de téléchargement de fichier via hello **/messages/servicebound/filenotifications** côté service de point de terminaison.

Au lieu de l’échange de messages via IoT Hub lui-même, IoT Hub au lieu de cela joue un tooan répartiteur associé compte de stockage Azure. Un périphérique demande un jeton de stockage à partir du IoT Hub qui est spécifique toohello fichier hello périphérique veut tooupload. Appareil de Hello utilise hello URI SAS tooupload hello fichier toostorage, et lorsque hello téléchargement est terminé appareil de hello envoie une notification d’achèvement tooIoT Hub. IoT Hub vérifie le téléchargement du fichier hello est terminé et qu’il ajoute ensuite un fichier téléchargement notification message toohello orientées service fichier notification point de terminaison.

Avant de télécharger un fichier de tooIoT Hub à partir d’un appareil, vous devez configurer votre concentrateur par [association d’un stockage Azure] [ lnk-associate-storage] tooit de compte.

Votre appareil peut ensuite [initialiser un téléchargement] [ lnk-initialize] , puis [notifier IoT hub] [ lnk-notify] quand le téléchargement de hello se termine. Si vous le souhaitez, lorsqu’un périphérique notifie IoT Hub téléchargement hello est terminée, service de hello peut générer un [message de notification][lnk-service-notification].

### <a name="when-toouse"></a>Lorsque toouse

Utilisez fichier télécharger toosend media les fichiers et les lots de télémétrie volumineux téléchargés par les appareils connectés par intermittence ou la bande passante toosave compressé.

Consultez trop[des conseils de communication de périphérique dans le cloud] [ lnk-d2c-guidance] en cas de doute entre l’utilisation des propriétés signalées, messages appareil-à-cloud ou téléchargement du fichier.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Association d’un compte Stockage Azure à IoT Hub

fonctionnalité de téléchargement de fichier toouse hello, vous devez d’abord lier un toohello de compte de stockage Azure IoT Hub. Vous pouvez effectuer cette tâche via hello [portail Azure][lnk-management-portal], ou par programmation via hello [fournisseur de ressources IoT Hub API REST] [ lnk-resource-provider-apis]. Une fois que vous avez associé un compte de stockage Azure à votre IoT Hub, hello service retourne un URI SAS tooa périphérique lors de l’appareil de hello initie une demande de téléchargement de fichier.

> [!NOTE]
> Hello [kits de développement logiciel Azure IoT] [ lnk-sdks] automatiquement la poignée de la récupération hello URI SAS, téléchargement du fichier de hello et la notification IoT Hub d’un téléchargement terminé.


## <a name="initialize-a-file-upload"></a>Initialiser un téléchargement de fichier
IoT Hub a un point de terminaison spécifiquement pour les périphériques toorequest un URI SAS pour tooupload de stockage un fichier. processus de téléchargement de fichier tooinitiate hello, appareil de hello envoie une demande POST trop`{iot hub}.azure-devices.net/devices/{deviceId}/files` avec hello suivant le corps JSON :

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

IoT Hub renvoie hello données, quel périphérique hello utilise le fichier de hello tooupload suivantes :

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>Déconseillé : initialiser un téléchargement de fichier avec une commande GET

> [!NOTE]
> Cette section décrit les fonctionnalités déconseillées de façon tooreceive un SAS URI à partir de IoT Hub. Utiliser la méthode POST de hello décrit précédemment.

IoT Hub a deux fichiers toosupport de points de terminaison REST hello tooget un URI SAS pour le stockage, téléchargez et hello autres concentrateur de IoT hello toonotify d’un téléchargement terminé. Hello appareil lance les processus de téléchargement de fichier hello en envoyant un concentrateur de IoT GET toohello à `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. IoT hub de Hello retourne :

* URI SAS spécifique toohello fichier toobe téléchargé.
* Un ID de corrélation toobe utilisé une fois le téléchargement de hello est terminé.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>Notifier IoT Hub de la fin du téléchargement d’un fichier

Appareil de Hello est chargé pour le téléchargement hello toostorage de fichier à l’aide du SDK de stockage Azure hello. Lorsque le téléchargement de hello est terminé, les appareils hello envoie une demande POST trop`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` avec hello suivant le corps JSON :

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

Hello valeur `isSuccess` est une valeur Boolean indiquant si le fichier de hello a été téléchargé correctement. Hello le code d’état de `statusCode` est hello d’état de téléchargement de hello de hello fichier toostorage et hello `statusDescription` correspond toohello `statusCode`.

## <a name="reference-topics"></a>Rubriques de référence :

Hello rubriques de référence suivantes vous fournissent plus d’informations sur le téléchargement de fichiers à partir d’un appareil.

## <a name="file-upload-notifications"></a>Notifications de téléchargement de fichier

Éventuellement, lorsqu’un périphérique avertit IoT Hub qu’un téléchargement est terminé, IoT Hub peut générer un message de notification qui contient l’emplacement de stockage et le nom hello du fichier de hello.

Comme l’explique la section [Points de terminaison][lnk-endpoints], IoT Hub fournit des notifications de chargement de fichiers sous la forme de messages par le biais d’un point de terminaison côté service (**/messages/servicebound/fileuploadnotifications**). sémantique de réception Hello pour les notifications de téléchargement de fichier sont hello même que pour les messages cloud-à-appareil et avez hello même [cycle de vie du message][lnk-lifecycle]. Chaque message récupérée à partir du point de terminaison de la notification de téléchargement de hello fichier est un enregistrement JSON avec hello propriétés suivantes :

| Propriété | Description |
| --- | --- |
| EnqueuedTimeUtc |Horodatage indiquant quand la notification de hello a été créée. |
| deviceId |**DeviceId** de dispositif hello hello fichier a été téléchargé. |
| BlobUri |URI du fichier de hello téléchargé. |
| BlobName |Nom de hello le fichier téléchargé. |
| LastUpdatedTime |Horodatage indiquant quand hello dernière mise à jour. |
| BlobSizeInBytes |Taille de hello le fichier téléchargé. |

**Exemple**. Cet exemple montre le corps hello de télécharger le message de notification.

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a>Options de configuration de notification de téléchargement de fichier

Chaque hub IoT expose hello des options de configuration pour les notifications de téléchargement de fichier suivantes :

| Propriété | Description | Plage et valeur par défaut |
| --- | --- | --- |
| **enableFileUploadNotifications** |Contrôle si les notifications de téléchargement de fichier sont écrits de point de terminaison notifications toohello fichier. |Valeur booléenne. Par défaut : True. |
| **fileNotifications.ttlAsIso8601** |Durée de vie par défaut des notifications de téléchargement de fichier. |Intervalle de ISO_8601 des too48H (au minimum 1 minute). Par défaut : 1 heure. |
| **fileNotifications.lockDuration** |Durée de verrouillage pour la file d’attente des notifications de téléchargement de fichier hello. |too300 5 secondes (5 secondes au minimum). Par défaut : 60 secondes. |
| **fileNotifications.maxDeliveryCount** |Nombre maximal de diffusions pour le fichier de hello télécharger la file d’attente de notification. |1 too100. Par défaut : 100. |

## <a name="additional-reference-material"></a>Matériel de référence supplémentaire

Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :

* [Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.
* [Limitation et les quotas] [ lnk-quotas] décrit les quotas hello et la limitation des comportements qui s’appliquent toohello IoT Hub service.
* [Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.
* [Langage de requête IoT Hub] [ lnk-query] décrit le langage de requête hello vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux.
* [Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.

## <a name="next-steps"></a>Étapes suivantes

Maintenant vous avez appris comment tooupload des fichiers à partir d’appareils à l’aide de IoT Hub, vous intéresser hello IoT Hub développeur guide rubriques suivantes :

* [Gérer les identités des appareils dans IoT Hub][lnk-devguide-identities]
* [Contrôle l’accès tooIoT Hub][lnk-devguide-security]
* [Utiliser les configurations et état du périphérique jumeaux toosynchronize][lnk-devguide-device-twins]
* [Appeler une méthode directe sur un appareil][lnk-devguide-directmethods]
* [Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]

Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant IoT Hub didacticiel :

* [Fichiers tooupload à partir d’appareils toohello de cloud avec IoT Hub][lnk-fileupload-tutorial]

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
