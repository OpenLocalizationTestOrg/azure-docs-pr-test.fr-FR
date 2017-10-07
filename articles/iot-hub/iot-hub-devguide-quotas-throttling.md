---
title: les quotas aaaUnderstand Azure IoT Hub et la limitation | Documents Microsoft
description: "Guide du développeur - description de quotas hello qui s’appliquent tooIoT Hub et hello attendu de comportement de limitation."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Référence - Quotas et limitation IoT Hub

## <a name="quotas-and-throttling"></a>Quotas et limitation
Chaque abonnement Azure peut avoir au maximum 10 IoT Hubs, et au maximum un hub gratuit.

Chaque IoT Hub est configuré avec un certain nombre d’unités dans une référence SKU spécifique (pour plus d’informations, consultez [Tarification Azure IoT Hub][lnk-pricing]). Hello référence (SKU) et le nombre d’unités déterminent hello maximale quotidienne de quota de messages que vous pouvez envoyer.

Hello référence (SKU) détermine également hello limites IoT Hub applique sur toutes les opérations.

## <a name="operation-throttles"></a>Limitations d’opérations
Limitations de l’opération sont les limites de taux qui sont appliquées dans les plages minute hello et qui sont destinés tooavoid abus. IoT Hub essaie tooavoid renvoie des erreurs chaque fois que possible, mais il commence à retourner des exceptions si la limitation de bande passante hello est violée trop longtemps.

Hello suivant table affiche hello appliquée accélérateurs. Les valeurs font référence hub individuels de tooan.

| Limitation | Hubs gratuits et S1 | Hubs S2 | Hubs S3 | 
| -------- | ------- | ------- | ------- |
| Opérations de registre des identités (création, récupération, création de listes, mise à jour, suppression) | 1,67/s/unité (100/min/unité) | 1.67/s/unité (100/min/unité) | 83,33/s/unité (5 000/min/unité) |
| Connexions d’appareils | 100/s ou 12/s/unité maximum <br/> Par exemple, deux unités S1 équivalent à 2\*12 = 24/s, mais vous obtenez au moins 100/s sur vos unités. Avec neuf unités S1, vous obtenez 108/sec (9\*12) sur vos unités. | 120/s/unité | 6 000/s/unité |
| Envois appareil-à-cloud | 100/s ou 12/s/unité maximum <br/> Par exemple, deux unités S1 équivalent à 2\*12 = 24/s, mais vous obtenez au moins 100/s sur vos unités. Avec neuf unités S1, vous obtenez 108/sec (9\*12) sur vos unités. | 120/s/unité | 6 000/s/unité |
| Envois cloud-à-appareil | 1.67/s/unité (100/min/unité) | 1.67/s/unité (100/min/unité) | 83.33/s/unité (5 000/min/unité) |
| Réceptions cloud-à-appareil <br/> (uniquement lorsque l’appareil utilise HTTP)| 16.67/s/unité (1 000/min/unité) | 16.67/s/unité (1 000/min/unité) | 833.33/s/unité (50 000/min/unité) |
| Chargement de fichiers | 1.67 notifications de téléchargement de fichier/s/unité (100/min/unité) | 1.67 notifications de téléchargement de fichier/s/unité (100/min/unité) | 83.33 notifications de téléchargement de fichier/s/unité (5 000/min/unité) |
| Méthodes directes | 20/s/unité | 60/s/unité | 3 000/s/unité | 
| Lectures de représentations d’appareil | 10/s | 10/s ou 1/s/unité maximum | 50/s/unité |
| Mises à jour de jumeaux d’appareils | 10/s | 10/s ou 1/s/unité maximum | 50/s/unité |
| Opérations de travaux <br/> (créer, mettre à jour, répertorier, supprimer) | 1.67/s/unité (100/min/unité) | 1.67/s/unité (100/min/unité) | 83.33/s/unité (5 000/min/unité) |
| Débit d’opérations de travaux par appareil | 10/s | 10/s ou 1/s/unité maximum | 50/s/unité |

Il est important tooclarify qui hello *les connexions d’appareils* taux hello à laquelle les nouvelles connexions d’appareil peuvent être établies avec un hub IoT détermine la limitation de bande passante. Hello *les connexions d’appareils* limitation de bande passante ne gère pas le nombre maximal de hello des périphériques connectés simultanément. limitation de bande passante Hello dépend du nombre hello d’unités qui sont configurés pour le hub IoT de hello.

Par exemple, si vous achetez une seule unité S1, vous obtenez une limitation de 100 connexions par seconde. Par conséquent, tooconnect 100 000 appareils, il prend au moins 1 000 secondes (environ 16 minutes). Toutefois, vous pouvez avoir autant d’appareils connectés simultanément que d’appareils enregistrés dans le registre des identités.

Pour une discussion détaillée de IoT Hub de limitation, consultez hello billet de blog [IoT Hub la limitation et vous][lnk-throttle-blog].

> [!NOTE]
> À un moment donné, il est possible tooincrease quotas ou limiter les limites en augmentant le nombre de hello d’unités configurées dans un hub IoT.
> 
> [!IMPORTANT]
> Les opérations de registre des identités sont prévues pour une utilisation au moment de l’exécution dans les scénarios de gestion et d’approvisionnement des appareils. La lecture ou la mise à jour d’un grand nombre d’identités d’appareils est prise en charge par le biais des [travaux d’importation et d’exportation][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Autres limites

IoT Hub impose d’autres limites opérationnelles :

| Opération | Limite |
| --------- | ----- |
| URI de chargement de fichiers | 10 000 URI de SAP peuvent être générés à la fois pour un compte de stockage. <br/> 10 URI de signature d’accès partagé/appareil peuvent être générés à la fois. |
| Tâches | Historique des travaux est conservé too30 jours <br/> Le nombre maximal de travaux simultanés est 1 (pour les niveaux gratuit et S1), 5 (pour S2) ou 10 (pour S3). |
| Points de terminaison supplémentaires | Les hubs avec SKU payants peuvent avoir 10 points de terminaison supplémentaires. Les hubs avec SKU gratuits peuvent avoir un point de terminaison supplémentaire. |
| Règles de routage de messages | Les hubs avec SKU payants peuvent avoir 100 règles de routage. Les hubs avec SKU gratuits peuvent avoir cinq règles de routage. |
| Messages d’appareil-à-cloud | Taille maximale des messages 256 Ko |
| Messages de cloud-à-appareil | Taille maximale des messages 64 Ko |
| Messages de cloud-à-appareil | Le nombre maximal de messages en attente de remise est 50 |

> [!NOTE]
> Actuellement, hello nombre maximal de périphériques que vous pouvez vous connecter tooa unique IoT hub est de 500 000. Si vous souhaitez tooincrease cette limite, contactez [Support technique de Microsoft](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Latency
IoT Hub s’efforce tooprovide faible latence pour toutes les opérations. Toutefois, en raison de conditions de toonetwork et d’autres facteurs imprévisibles, il ne peut pas garantir une latence maximale. Lorsque vous concevez votre solution, vous devez :

* Évitez de faire d’hypothèses sur la latence maximale de hello de toute opération d’IoT Hub.
* Configurer votre concentrateur IoT appareils tooyour le plus proche de hello région Azure.
* Envisagez d’utiliser Azure IoT bord tooperform raison d’opérations sensibles sur l’appareil de hello ou sur un périphérique de fermer toohello de passerelle.

Plusieurs unités IoT Hub affectent la limitation comme décrit précédemment, mais ne fournissent pas d’avantages ni de garanties supplémentaires en termes de latence.
Si vous constatez des augmentations inattendues de la latence des opérations, contactez le [Support Microsoft](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Étapes suivantes
Les autres rubriques de référence de ce Guide du développeur IoT Hub comprennent :

* [Points de terminaison IoT Hub][lnk-devguide-endpoints]
* [Langage de requête IoT Hub les jumeaux d’appareils, les travaux et le routage des messages][lnk-devguide-query]
* [Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
