---
title: filtres de connexion IoT Hub IP aaaAzure | Documents Microsoft
description: "Comment les adresses IP de toouse tooblock des connexions à partir de l’adresse IP spécifique de filtrage pour tooyour Azure IoT hub. Vous pouvez bloquer les connexions à partir d’adresses IP individuelles ou de plages d’adresses IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>Utiliser des filtres IP

La sécurité est un aspect important de toute solution IoT basée sur Azure IoT Hub. Vous devez parfois tooexplicitly spécifier hello, adresses de base de données à partir de laquelle les appareils peuvent se connecter en tant que partie de votre configuration de sécurité. Hello _filtre IP_ fonctionnalité vous permet de tooconfigure les règles de refus ou accepter le trafic provenant de certaines adresses IPv4.

## <a name="when-toouse"></a>Lorsque toouse

Il existe deux cas d’utilisation spécifiques lorsqu’il est utile de tooblock hello IoT Hub points de terminaison pour certaines adresses IP :

- Votre IoT Hub ne doit recevoir du trafic qu’à partir d’une plage spécifiée d’adresses IP et rejeter tout le reste. Par exemple, vous utilisez votre IoT hub avec [Azure Expressroute] toocreate des connexions privées entre un IoT hub et votre infrastructure locale.
- Vous devez le trafic de tooreject à partir d’adresses IP qui ont été identifiées comme suspecte par l’administrateur de hub IoT hello.

## <a name="how-filter-rules-are-applied"></a>Application des règles de filtre

règles de filtre IP Hello sont appliqués au hello au niveau du service IoT Hub. Par conséquent, les règles de filtre IP hello appliquent tooall des connexions à partir de périphériques et les applications de serveur principal à l’aide de n’importe quel protocole pris en charge.

Toute tentative de connexion à partir d’une adresse IP qui correspond à une règle IP de rejet dans votre IoT Hub reçoit un code d’état 401 non autorisé et une description. message de réponse Hello ne mentionne pas la règle d’adresse IP hello.

## <a name="default-setting"></a>Paramètre par défaut

Par défaut, hello **filtre IP** grille dans le portail hello pour un hub IoT est vide. Ce paramètre par défaut signifie que votre concentrateur accepte les connexions de n’importe quelle adresse IP. Ce paramètre par défaut est la règle tooa équivalente qui accepte une plage d’adresses IP hello 0.0.0.0/0.

![Paramètres de filtre IP par défaut d’IoT Hub][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>Ajouter ou modifier une règle de filtre IP

Lorsque vous ajoutez une règle de filtrage IP, vous êtes invité pour hello valeurs suivantes :

- Un **nom de règle de filtre IP** qui doit être une chaîne alphanumérique, unique et pas la casse des caractères too128. Seul hello ASCII 7 bits des caractères alphanumériques plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` sont acceptées.
- Sélectionnez un **rejeter** ou **accepter** comme hello **action** pour la règle de filtre IP hello.
- Fournissez une adresse IPv4 unique ou un bloc d’adresses IP en notation CIDR. Par exemple, CIDR notation 192.168.100.0/22 représente des adresses IPv4 hello 1024 provenant de 192.168.100.0 too192.168.103.255.

![Ajouter un hub IoT tooan de règle de filtre IP][img-ip-filter-add-rule]

Après avoir enregistré la règle de hello, vous voyez une alerte vous informe de que cette mise à jour hello est en cours d’exécution.

![Notification sur l’enregistrement d’une règle de filtre IP][img-ip-filter-save-new-rule]

Hello **ajouter** option est désactivée lorsque vous atteignez au maximum 10 règles de filtre IP hello.

Vous pouvez modifier une règle existante en double-cliquant sur la ligne hello qui contient la règle de hello.

> [!NOTE]
> Rejet IP adresses peuvent empêcher des autres Services Azure (par exemple, Analytique de flux de données Azure, les Machines virtuelles Azure ou hello Explorateur de périphérique dans le portail de hello) d’interagir avec IoT hub de hello.

> [!WARNING]
> Si vous utilisez des messages de tooread Analytique de flux de données Azure (ASA) à partir d’un IoT hub avec le filtrage IP est activé, utiliser le nom du concentrateur d’événements compatibles hello et le point de terminaison de votre IoT Hub Bonjour chaîne de connexion ASA.

## <a name="delete-an-ip-filter-rule"></a>Suppression d’une règle de filtre IP

toodelete une règle de filtre IP, sélectionnez une ou plusieurs règles dans la grille de hello et cliquez sur **supprimer**.

![Supprimer une règle de filtre IP de l’IoT Hub][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>Évaluation de règle de filtre IP

Les règles de filtre IP sont appliquées dans l’ordre et hello première règle que correspondances hello adresse détermine hello accepter ou rejeter l’action.

Par exemple, si vous voulez les adresses tooaccept hello plage 192.168.100.0/22 rejetez tout le reste, hello première règle de grille de hello doit accepter hello adresse plage 192.168.100.0/22. règle de Hello suivante doit rejeter toutes les adresses à l’aide de 0.0.0.0/0 de la plage hello.

Vous pouvez modifier l’ordre hello de vos règles de filtre IP dans la grille de hello en cliquant sur trois points verticaux hello au début de hello d’une ligne par glisser- déposer.

votre nouvelle adresse IP de filtre toosave ordre des règles, cliquez sur **enregistrer**.

![Modifier l’ordre de vos règles de filtre IP du Hub IoT hello][img-ip-filter-rule-order]

## <a name="next-steps"></a>Étapes suivantes

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

- [Surveillance des opérations][lnk-monitor]
- [Métriques d’IoT Hub][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Expressroute]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md