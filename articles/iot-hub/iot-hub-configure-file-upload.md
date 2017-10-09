---
title: "téléchargement du fichier aaaUse hello tooconfigure portail Azure | Documents Microsoft"
description: "Comment toouse hello tooconfigure portail Azure votre fichier tooenable de hub IoT télécharge à partir d’appareils connectés. Inclut des informations sur la configuration du compte de stockage Azure hello destination."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>Configurer des téléchargements de fichiers IoT Hub à l’aide de hello portail Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Chargement de fichiers

toouse hello [fonctionnalité de téléchargement de fichiers dans le IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure avec votre concentrateur. Sélectionnez **téléchargement du fichier** toodisplay une liste de propriétés de téléchargement de fichier pour le hub IoT hello qui est en cours de modification.

![Afficher le fichier IoT Hub télécharger les paramètres dans le portail de hello][13]

**Conteneur de stockage**: utilisez hello tooselect portail Azure un conteneur d’objets blob dans un compte de stockage Azure dans votre tooassociate abonnement Azure actuel avec votre IoT Hub. Si il nécessaire, vous pouvez créer un compte Azure Storage sur hello **comptes de stockage** conteneur lame et d’objets blob sur hello **conteneurs** panneau. IoT Hub génère automatiquement les URI de SAS avec le conteneur d’objets blob toothis écriture des autorisations pour les appareils toouse lorsqu’ils téléchargent des fichiers.

![Afficher les conteneurs de stockage pour le téléchargement du fichier dans le portail de hello][14]

**Recevoir des notifications pour les fichiers téléchargés**: activer ou désactiver les notifications de téléchargement de fichier par le biais bascule de hello.

**SAS TTL**: ce paramètre est hello time-to-live de hello SAS URI retourné toohello appareil par IoT Hub. Heure de tooone la valeur par défaut, mais peuvent être personnalisé tooother valeurs à l’aide de curseur de hello.

**Fichier de paramètres par défaut de durée de vie de notification**: hello time-to-live d’une notification de téléchargement de fichier avant son expiration. Jour de tooone la valeur par défaut, mais peuvent être personnalisé tooother valeurs à l’aide de curseur de hello.

**Nombre maximal de diffusions de notification de fichiers**: hello fréquence hello IoT Hub tentatives toodeliver une notification de téléchargement de fichier. Too10 la valeur par défaut, mais peuvent être personnalisé tooother valeurs à l’aide de curseur de hello.

![Configurer le téléchargement du fichier IoT Hub dans le portail de hello][15]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les fonctionnalités de téléchargement de fichier hello IoT Hub, consultez [télécharger des fichiers à partir d’un appareil] [ lnk-upload] Bonjour guide du développeur IoT Hub.

Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :

* [Gérer en bloc des appareils IoT][lnk-bulk]
* [Métriques d’IoT Hub][lnk-metrics]
* [Surveillance des opérations][lnk-monitor]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]
* [Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
