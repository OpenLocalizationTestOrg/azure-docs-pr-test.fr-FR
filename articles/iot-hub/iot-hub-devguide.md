---
title: "guide d’aaaDeveloper pour Azure IoT Hub | Documents Microsoft"
description: "guide du développeur Azure IoT Hub Hello comprend des discussions de points de terminaison, sécurité, Registre des identités hello, gestion des périphériques, méthodes directes, jumeaux de périphérique, des téléchargements de fichiers, travaux, hello langage de requête IoT Hub et la messagerie."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Guide du développeur Azure IoT Hub

Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.

Azure IoT Hub vous offre :

* La sécurité des communications grâce aux informations d’identification de sécurité par appareil et au contrôle d’accès
* Plusieurs options de communication appareil-à-cloud et cloud-à-appareil à très grande échelle.
* Stockage requêtable de métadonnées et d’informations d’état par appareil.
* Connectivité des périphériques facile avec les bibliothèques de périphérique pour les plateformes et les langues les plus populaires hello.

Ce guide du développeur IoT Hub inclut hello suivant des articles :

* [L’aide sur la communication appareil-à-cloud][lnk-d2c-guidance] vous permet de choisir entre les messages appareil-à-cloud, les propriétés signalées des représentations d’appareil et le chargement de fichiers.
* [L’aide sur la communication cloud-à-appareil][lnk-c2d-guidance] vous permet de choisir entre les méthodes directes, les propriétés souhaitées des jumeaux d’appareil et les messages cloud-à-appareil.
* [Appareil-à-cloud et messagerie avec IoT Hub cloud-à-appareil] [ devguide-messaging] décrit hello fonctionnalités de messagerie (appareil-à-cloud et cloud-à-appareil) qui expose de IoT Hub.
  * [Envoyer des messages appareil-à-cloud tooIoT Hub][devguide-messages-d2c].
  * [Lire des messages de l’appareil-à-cloud à partir du point de terminaison intégrés hello][devguide-builtin].
  * [Utiliser des points de terminaison et des règles de routage personnalisés pour les messages appareil-à-cloud][devguide-custom].
  * [Envoyer des messages cloud-à-appareil à partir d’IoT Hub][devguide-messages-c2d].
  * [Créer et lire des messages IoT Hub][devguide-format].
* L’article [Charger des fichiers à partir d’un appareil][devguide-upload] décrit la façon dont vous pouvez charger des fichiers à partir d’un appareil. Hello inclut également des informations sur des sujets tels que hello peuvent envoyer des notifications de processus de téléchargement hello.
* L’article [Gérer les identités des appareils dans IoT Hub][devguide-identities] décrit les informations stockées par chaque registre des identités d’IoT Hub, ainsi que la manière d’y accéder et de les modifier.
* [Contrôler l’accès tooIoT Hub] [ devguide-security] décrit hello sécurité modèle utilisé toogrant tooIoT Hub fonctionnalité d’accès pour les périphériques et les composants de nuage. Hello inclut des informations sur l’utilisation de jetons et des certificats X.509 et des détails de que vous pouvez accorder des autorisations hello.
* [Utiliser les configurations et état du périphérique jumeaux toosynchronize] [ devguide-device-twins] décrit hello *double de l’appareil* concept et hello des fonctionnalités telles que la synchronisation d’un périphérique avec son appareil, elle expose Double. Hello inclut des informations sur les données hello stockées dans un double de l’appareil.
* [Appeler une méthode directe sur un appareil] [ devguide-directmethods] décrit hello du cycle de vie d’une méthode directe, plus d’informations sur la façon dont méthodes tooinvoke sur un appareil à partir de votre hello d’application et le handle principal méthode directe sur votre appareil.
* L’article [Planifier des travaux sur plusieurs appareils][devguide-jobs] décrit la manière dont vous pouvez planifier des travaux sur plusieurs appareils. Hello explique comment toosubmit des tâches qu’effectuer des tâches que l’exécution d’une méthode directe, mise à jour d’un périphérique à l’aide d’un double de l’appareil. Elle décrit également comment tooquery hello état d’un travail.
* [Référence : choisissez un protocole de communication] [ devguide-protocol] décrit les protocoles de communication hello que IoT Hub prend en charge pour la communication de l’appareil et listes hello ports doivent être ouverts.
* [Une référence - points de terminaison IoT Hub] [ devguide-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations d’exécution et de gestion. Hello décrit également comment vous pouvez créer des points de terminaison supplémentaires dans votre IoT hub et toouse une passerelle champ tooenable les tooyour de connectivité d’appareils IoT Hub points de terminaison dans les scénarios non standard.
* [Référence de langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages -] [ devguide-query] décrit ce langage de requête IoT Hub qui vous permet de tooretrieve informations à partir de votre concentrateur votre jumeaux de périphérique et les travaux.
* [Une référence - quotas et la limitation] [ devguide-quotas] résume les quotas hello définis dans hello IoT Hub service et hello comportement toosee quand vous dépassez un quota de limitation.
* [Référence - tarification] [ devguide-pricing] fournit des informations générales sur les différentes références (SKU) et les tarifs de IoT Hub et plus d’informations sur comment hello diverses fonctionnalités IoT Hub sont contrôlées en tant que messages par IoT Hub.
* [Une référence - périphérique et le service SDK] [ devguide-sdks] listes hello les kits de développement Azure IoT vous pouvez utiliser toodevelop périphérique et service des applications qui interagissent avec votre IoT hub. Hello inclut une documentation tooonline API de liens.
* [Une référence - prise en charge IoT Hub MQTT] [ devguide-mqtt] fournit des informations détaillées sur comment IoT Hub prend en charge le protocole MQTT hello. article de Hello décrit hello MQTT protocole intégré toohello kits de développement logiciel Azure IoT hello prise en charge et fournit des informations sur l’utilisation de protocole MQTT hello directement.
* [Glossaire][devguide-glossary] contient une liste des termes courants relatifs à IoT Hub.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
