---
title: "aaaAzure IoT Hub haute disponibilité et récupération d’urgence | Documents Microsoft"
description: "Décrit les fonctionnalités d’Azure et IoT Hub hello qui vous aident à toobuild des solutions Azure IoT hautement disponibles avec les fonctionnalités de récupération d’urgence."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>Haute disponibilité et récupération d’urgence IoT Hub :
Comme un service Azure, IoT Hub offre une haute disponibilité (HA) à l’aide de redondances au niveau des régions Azure hello, sans aucun travail supplémentaire requis par la solution de hello. plateforme de Microsoft Azure Hello inclut également toohelp fonctionnalités développer des solutions avec les fonctionnalités de récupération d’urgence ou entre régions disponibilité. Si vous souhaitez tooprovide global, entre régions haute disponibilité pour les périphériques ou utilisateurs, concevoir et préparer vos solutions parti tootake de ces fonctionnalités de récupération d’urgence Azure. article de Hello [aide technique la continuité des activités Azure](../resiliency/resiliency-technical-guidance.md) décrit hello des fonctionnalités intégrées dans Azure pour la continuité d’activité et de récupération d’urgence. Hello [la récupération d’urgence et haute disponibilité pour les applications Azure] [ Disaster recovery and high availability for Azure applications] livre fournit Guide d’architecture sur les stratégies pour les applications Azure tooachieve haute disponibilité et récupération d’urgence.

## <a name="azure-iot-hub-dr"></a>Récupération d’urgence Azure IoT Hub
De plus haute disponibilité toointra-région, IoT Hub implémente des mécanismes de basculement pour la récupération d’urgence qui ne requièrent aucune intervention de l’utilisateur de hello. Récupération d’urgence de Hub IoT est lancée automatiquement et a un objectif de temps de récupération (RTO) de 2-26 heures et hello suivant des objectifs de point de récupération (RPO).

| Fonctionnalités | RPO |
| --- | --- |
| Disponibilité du service pour les opérations de Registre et de communication |Perte éventuelle du CName |
| Données d’identité dans le registre des identités |Perte de données entre 0 et 5 minutes |
| Messages appareil-à-cloud |Perte de tous les messages non lus |
| Messages de surveillance des opérations |Perte de tous les messages non lus |
| Messages cloud-à-appareil |Perte de données entre 0 et 5 minutes |
| File d’attente de rétroaction cloud-à-appareil |Perte de tous les messages non lus |

## <a name="regional-failover-with-iot-hub"></a>Basculement régional avec IoT Hub
Un traitement complet des topologies de déploiement dans les solutions IoT est en dehors de la portée de hello de cet article. Hello explique hello *basculement régional* modèle de déploiement pour l’objectif de hello de haute disponibilité et récupération d’urgence.

Dans un modèle de basculement régional, hello solution précédent s’exécute principalement dans l’emplacement d’un centre de données, et un secondaire IoT hub et le serveur principal sont déployés dans un autre emplacement de centre de données. Si hello IoT hub dans le centre de données principal hello subit une panne ou hello la connectivité réseau à partir de hello appareil toohello centre de données principal est interrompue. Les appareils utilisent un point de terminaison secondaire, chaque fois que la passerelle principale du hello ne peut pas être atteint. Avec une capacité de basculement entre régions, disponibilité de la solution hello peut être améliorée au-delà de la haute disponibilité de hello d’une seule région.

À un niveau élevé, tooimplement un modèle de basculement régional avec IoT Hub, vous hello éléments suivants sont nécessaires :

* **Un IoT hub et un périphérique logique de routage secondaire**: dans le cas de hello d’une interruption de service dans votre région primaire, appareils doivent démarrer connexion tooyour la région secondaire. Étant donné hello nature état prenant en charge de la plupart des services impliqués, il est courant pour les processus de basculement de la région de solution administrateurs tootrigger hello. Bonjour meilleure manière toocommunicate hello nouveau point de terminaison toodevices, tout en conservant le contrôle du processus de hello, est toohave les vérifier régulièrement un *conseiller* service pour le point de terminaison actif actuel hello. Hello conseiller service peut être une application web qui est répliquée et conservée n’est accessible à l’aide de techniques de la redirection DNS (par exemple, à l’aide de [Azure Traffic Manager][Azure Traffic Manager]).
* **Réplication du Registre identité** -toobe utilisable, hub IoT secondaire de hello doit contenir toutes les identités des appareils qui peuvent se connecter toohello solution. solution de Hello doit conserver les sauvegardes de géo-répliquées des identités d’appareil et les télécharger toohello secondaire IoT hub avant de basculer le point de terminaison actif hello pour les appareils hello. fonctionnalité d’exportation Hello appareil identité de IoT Hub est utile dans ce contexte. Pour plus d’informations, consultez[Guide du développeur IoT Hub - Registre des identités][IoT Hub developer guide - identity registry].
* **La fusion logique** - lorsque la région primaire hello redevient disponible, toutes hello état et les données qui ont été créées dans le site secondaire de hello doivent être migrés toohello précédent la région primaire. Cet état et les données concerne principalement les identités toodevice et les métadonnées de l’application, qui doivent être fusionnée avec hello principal IoT hub et de tous les autres magasins spécifiques à l’application dans la région principale de hello. toosimplify cette étape, vous devez utiliser les opérations idempotent. Idempotent opérations réduire hello des effets de distribution de cohérence éventuelle hello d’événements et des doublons ou hors de livraison d’événements. En outre, la logique d’application hello doit être conçue tootolerate les incohérences potentielles ou « légèrement « état de la date. Cette situation peut se produire en raison de toohello de temps supplémentaire que nécessaire pour le système de hello trop « réparer » basé sur les objectifs de point de récupération (RPO).

## <a name="next-steps"></a>Étapes suivantes
Suivez ces liens de toolearn plus d’informations sur Azure IoT Hub :

* [Prise en main des IoT Hubs (didacticiel)][lnk-get-started]
* [Qu’est-ce qu’Azure IoT Hub ?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
