---
title: "tarification d’Azure IoT Hub aaaUnderstand | Documents Microsoft"
description: "Guide du développeur : informations concernant le fonctionnement des mesures et des tarifs IoT Hub, avec des exemples."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Informations sur les tarifs Azure IoT Hub

[IoT Hub Azure tarification] [ lnk-pricing] fournit des informations générales de hello sur différentes références (SKU) et les tarifs de IoT Hub. Cet article contient plus d’informations sur comment hello que diverses fonctionnalités IoT Hub sont contrôlées en tant que messages par IoT Hub.

## <a name="charges-per-operation"></a>Frais par opération

| Opération | Informations de facturation | 
| --------- | ------------------- |
| Opérations du registre d’identité <br/> (créer, récupérer, répertorier, mettre à jour, supprimer) | Non facturé. |
| Messages appareil-à-cloud | Les messages envoyés avec succès sont facturés en blocs de 4 Ko lors de l’entrée dans IoT Hub ; par exemple, un message de 6 Ko est facturé 2 messages. |
| Messages cloud-à-appareil | Les messages envoyés avec succès sont facturés en blocs de 4 Ko ; par exemple, un message de 6 Ko est facturé 2 messages. |
| Chargements de fichiers | Transfert de fichier tooAzure stockage n’est pas limitée par IoT Hub. Les messages de lancement et de complétion du transfert de fichiers sont facturés en tant que messages, par incréments de 4 Ko. Par exemple, le transfert d’un fichier de 10 Mo est facturé deux messages dans Ajout toohello le coût de stockage Azure. |
| Méthodes directes | Les demandes réussies de méthodes sont facturées par blocs de 4 Ko, tandis que les réponses comportant des corps non vides sont elles aussi facturées par blocs de 4 Ko, en tant que messages supplémentaires. Les appareils toodisconnected demandes sont facturées comme des messages dans des segments de 4 Ko. Par exemple, une méthode avec un corps de 6 Ko qui résulte dans une réponse sans corps hello périphérique, est facturé comme deux messages ; une méthode avec un corps de 6 Ko qui résulte dans une réponse de 1 Ko à partir de l’appareil de hello est facturée comme deux messages de demande de hello et un autre message de réponse de hello. |
| Lectures de représentations d’appareil | Double de l’appareil lit à partir de l’appareil de hello et de solution hello précédent fin sont facturées comme des messages dans des segments de 512 octets. Par exemple, la lecture d’un jumeau d’appareil de 6 Ko est facturée en tant que 12 messages. |
| Mises à jour de jumeaux d’appareil (balises et propriétés) | Mises à jour d’appareil double à partir de hello et hello périphérique sont facturées comme des messages dans des segments de 512 octets. Par exemple, la lecture d’un jumeau d’appareil de 6 Ko est facturée en tant que 12 messages. |
| Requêtes de jumeaux d’appareil | Les requêtes sont facturées comme des messages en fonction de la taille des résultats hello dans les blocs de 512 octets. |
| Opérations de travaux <br/> (créer, mettre à jour, répertorier, supprimer) | Non facturé. |
| Opérations de travaux par appareil | Les opérations de travaux (comme les mises à jour de jumeaux d’appareil et les méthodes) sont facturées normalement. Par exemple, un travail entraînant 1 000 appels de méthode avec des demandes de 1 Ko et des réponses à corps vide est facturé en tant que 1 000 messages. |

> [!NOTE]
> Toutes les tailles sont calculées prise en compte la taille de la charge hello en octets (la trame de protocole est ignoré). En cas de messages (qui possèdent des propriétés et corps) taille de hello est calculée de manière agnostique du protocole, comme décrit dans hello [IoT Hub guide du développeur de messagerie][lnk-message-size].

## <a name="example-1"></a>Exemple 1

Un périphérique envoie un message de périphérique dans le cloud de 1 Ko par minute tooIoT concentrateur, qui est ensuite lue par Analytique de flux de données Azure. Hello solution back-end appelle une méthode (avec une charge utile de 512 octets) sur le périphérique de hello chaque tootrigger dix minutes une action spécifique. Hello répond méthode toohello avec un résultat de 200 octets.

périphérique de Hello consomme 1 message * 60 minutes * 24 heures = 1440 de messages par jour pour les messages appareil-à-cloud hello et 2 demande et réponse * 6 fois par heure * 24 heures = 288 des messages pour les méthodes hello, pour un total de messages 1728 par jour.

## <a name="example-2"></a>Exemple n° 2

Chaque heure, un appareil envoie un message appareil-à-cloud de 100 Ko. Il met également à jour son jumeau d’appareil avec des charges utiles de 1 Ko toutes les 4 heures. solution de Hello précédent se terminer, une fois par jour, les lectures hello 14 Ko appareil double et met à jour avec des configurations de toochange de charges utiles de 512 octets.

périphérique de Hello consomme 25 messages (100 Ko/4 Ko) * 24 heures pour les messages appareil-à-cloud, ainsi que le 1 message * 6 fois par jour pour les mises à jour d’appareil double, pour un total de 156 messages par jour.
Hello back-end solution consomme double d’appareil (14 Ko/0,5 Ko) de 28 messages tooread hello, plus 1 message tooupdate il, pour un total de messages de 29.

Au total, l’appareil de hello et hello solution back-end consomment 185 messages par jour.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
