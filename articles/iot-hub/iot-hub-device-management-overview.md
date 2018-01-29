---
title: Gestion des appareils avec Azure IoT Hub | Microsoft Docs
description: "Vue d’ensemble de la gestion des appareils dans Azure IoT Hub : cycle de vie des appareils d’entreprise et modèles de gestion des appareils tels que redémarrage, réinitialisation aux paramètres d’usine, mise à jour du microprogramme, configuration, représentations d’appareil, requêtes et travaux."
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 458b316ba76ff7cace56eb21eaf105233e508741
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
---
# <a name="overview-of-device-management-with-iot-hub"></a>Vue d’ensemble de la gestion des appareils avec IoT Hub
## <a name="introduction"></a>Introduction
Azure IoT Hub fournit les fonctionnalités et un modèle d’extensibilité qui permettent aux développeurs d’appareils et de serveur principal de créer des solutions robustes de gestion des appareils. Les appareils englobent les capteurs de contraintes et les microcontrôleurs à un seul objectif, les passerelles puissantes qui acheminent les communications pour les groupes d’appareils.  En outre, les cas d’utilisation et la configuration requise pour les opérateurs IoT varient considérablement entre les industries.  Malgré cette variation, la gestion des appareils avec IoT Hub fournit les fonctionnalités, les modèles et les bibliothèques de code pour répondre aux besoins d’un ensemble varié d’appareils et d’utilisateurs finaux.

Une composante essentielle de la création d’une solution IoT d’entreprise efficace consiste à fournir une stratégie portant sur la manière dont les opérateurs assurent la gestion continue de leur collection d’appareils. Les opérateurs IoT ont besoin d’outils et d’applications à la fois simples et fiables qui leur permettent de se concentrer sur les aspects plus stratégiques de leur travail. Cet article fournit :

* Une brève vue d’ensemble de l’approche de gestion des appareils Azure IoT Hub.
* Une description des principes courants de gestion des appareils.
* Une description du cycle de vie de l’appareil.
* Une vue d’ensemble des modèles courants de gestion des appareils.

## <a name="device-management-principles"></a>Principes de gestion des appareils
L’IoT implique un ensemble unique de problèmes de gestion des appareils et chaque solution d’entreprise doit tenir compte des principes suivants :

![Graphique Principes de gestion des appareils][img-dm_principles]

* **Mise à l’échelle et automatisation** : les solutions IoT nécessitent des outils simples à même d’automatiser les tâches de routine et de permettre à un personnel opérationnel relativement réduit de gérer des millions d’appareils. Au quotidien, les opérateurs doivent pouvoir gérer les opérations d’appareils à distance, en bloc et être avertis uniquement lorsque les problèmes qui surviennent nécessitent leur attention directe.
* **Transparence et compatibilité** : l’écosystème d’appareils est incroyablement varié. Les outils de gestion doivent être adaptés pour prendre en charge une multitude de classes, de plateformes et de protocoles d’appareils. Les opérateurs doivent pouvoir prendre en charge de nombreux types d’appareils, depuis les puces intégrées limitées à processus unique jusqu’aux ordinateurs puissants et entièrement fonctionnels.
* **Prise en compte du contexte** : les environnements IoT sont dynamiques et en perpétuelle évolution. La fiabilité du service est primordiale. Les opérations de gestion d’appareils doivent prendre en compte les facteurs suivants pour garantir que les interruptions de maintenance n’affectent pas les opérations critiques et ne créent pas de conditions dangereuses :
    * Fenêtres de maintenance SLA
    * États du réseau et de l’alimentation
    * Conditions d’utilisation
    * Géolocalisation des appareils
* **Prise en charge de nombreux rôles** : la prise en charge des flux de travail et des processus uniques des rôles opérationnels liés à l’IoT est cruciale. Le personnel en charge des opérations doit travailler en harmonie avec les contraintes des services informatiques en interne.  Ils doivent également trouver des façons durables pour faire remonter les informations sur les opérations d’appareil en temps réel aux superviseurs et autres rôles de gestion dans l’entreprise.

## <a name="device-lifecycle"></a>Cycle de vie des appareils
Il existe un ensemble d’étapes de gestion d’appareils générale qui sont communes à tous les projets IoT d’entreprise. Dans Azure IoT, il existe cinq phases dans le cycle de vie des appareils :

![Les cinq phases du cycle de vie des appareils Azure IoT : planifier, approvisionner, configurer, surveiller, mettre hors service][img-device_lifecycle]

Dans chacune de ces cinq étapes, il existe plusieurs conditions destinées à l’opérateur des appareils qui doivent être respectées pour fournir une solution complète :

* **Planification** : permettre aux opérateurs de créer un schéma de métadonnées d’appareils afin qu’ils puissent facilement et précisément rechercher et cibler un groupe d’appareils pour les opérations de gestion en bloc. Vous pouvez utiliser la représentation physique d’appareil pour stocker les métadonnées de cet appareil sous la forme d’étiquettes et de propriétés.
  
    *Ressources supplémentaires* : [Prise en main des représentations d’appareils][lnk-twins-getstarted], [Comprendre les représentations d’appareils][lnk-twins-devguide], [Utilisation des propriétés des représentations][lnk-twin-properties].
* **Approvisionnement** : approvisionner les nouveaux appareils en toute sécurité auprès d’IoT Hub et permettre aux opérateurs de détecter immédiatement les fonctionnalités des appareils.  Utilisez le registre des identités IoT Hub pour créer des informations d’identification et des identités d’appareils flexibles et effectuez cette opération en bloc à l’aide d’un travail. Créez les appareils afin qu’ils signalent leurs fonctionnalités et leur condition via les propriétés de l’appareil dans la représentation d’appareil.
  
    *Ressources supplémentaires* : [Gérer les identités des appareils][lnk-identity-registry], [Gestion en bloc des identités d’appareils][lnk-bulk-identity], [Comment : Utiliser des propriétés de jumeau d’appareil][lnk-twin-properties], [Service d’approvisionnement d’appareils IoT Hub Azure][lnk-dps].
* **Configuration** : rendre possibles les modifications de configuration et les mises à jour de microprogramme en bloc sur les appareils, tout en assurant intégrité et sécurité. Effectuez ces opérations de gestion d’appareils en bloc à l’aide des propriétés requises ou de méthodes directes et de travaux de diffusion.
  
    *Ressources supplémentaires* :  [Utiliser des méthodes directes][lnk-c2d-methods], [Appeler des méthodes directes sur un appareil][lnk-methods-devguide], [Utilisation des propriétés des représentations][lnk-twin-properties], [Planifier et diffuser des travaux][lnk-jobs], [Planifier des travaux sur plusieurs appareils][lnk-jobs-devguide].
* **Surveillance** : surveiller l’intégrité globale de la collection d’appareils, l’état des opérations en cours et avertir les opérateurs des problèmes susceptibles de nécessiter leur attention.  Appliquez la représentation physique d’appareil pour autoriser les appareils à signaler des conditions de fonctionnement en temps réel et l’état des opérations de mise à jour. Créez des rapports de tableau de bord puissants qui font remonter les problèmes les plus immédiats à l’aide de requêtes sur la représentation physique d’appareil.
  
    *Ressources supplémentaires* : [Utilisation des propriétés souhaitées pour configurer des appareils (Node)][lnk-twin-properties], [Référence - Langage de requête d’IoT Hub pour les représentations d’appareil et les travaux][lnk-query-language].
* **Mise hors service** : remplacer ou retirer des appareils après une défaillance, un cycle de mise à niveau ou à la fin de leur durée de vie.  Utilisez la représentation d’appareil pour conserver les informations sur l’appareil si l’appareil physique est remplacé ou archivé en cas de mise hors service. Utilisez le registre des identités IoT Hub pour la révocation en toute sécurité des informations d’identification et des identités des appareils.
  
    *Ressources supplémentaires* : [Utilisation des propriétés des représentations][lnk-twin-properties], [Gérer les identités des appareils][lnk-identity-registry].

## <a name="device-management-patterns"></a>Modèle de gestion des appareils
IoT Hub permet de mettre en œuvre l’ensemble suivant de modèles de gestion des appareils.  Les [didacticiels de gestion des appareils][lnk-get-started] vous montrent plus en détail comment étendre ces modèles pour les adapter à votre situation et comment concevoir de nouveaux modèles basés sur ces modèles de base.

* **Redémarrage** : l’application principale informe l’appareil par le biais d’une méthode directe qu’un redémarrage a été lancé.  L’appareil utilise les propriétés signalées pour mettre à jour l’état de redémarrage de l’appareil.
  
    ![Graphique du modèle de redémarrage de la gestion des appareils][img-reboot_pattern]
* **Réinitialisation aux paramètres d’usine** : l’application principale informe l’appareil par le biais d’une méthode directe qu’une réinitialisation aux paramètres d’usine a été lancée.  L’appareil utilise les propriétés signalées pour mettre à jour l’état de réinitialisation aux paramètres d’usine de l’appareil.
  
    ![Graphique du modèle de réinitialisation aux paramètres d’usine de la gestion des appareils][img-facreset_pattern]
* **Configuration** : l’application principale utilise les propriétés souhaitées pour configurer le logiciel en cours d’exécution sur l’appareil.  L’appareil utilise les propriétés signalées pour mettre à jour l’état de configuration de l’appareil.
  
    ![Graphique du modèle de configuration de la gestion des appareils][img-config_pattern]
* **Mise à jour du microprogramme** : l’application principale informe l’appareil par le biais d’une méthode directe qu’une mise à jour du microprogramme a été lancée.  L’appareil met en œuvre un processus en plusieurs étapes pour télécharger l’image du microprogramme, appliquer cette image et enfin se reconnecter au service IoT Hub.  Tout au long de ce processus en plusieurs étapes, l’appareil utilise les propriétés signalées pour mettre à jour la progression et l’état de l’appareil.
  
    ![Graphique du modèle de mise à jour du microprogramme de la gestion des appareils][img-fwupdate_pattern]
* **Signalement de la progression et de l’état** : le serveur principal de solution exécute des requêtes de représentation d’appareil sur un ensemble d’appareils afin de rendre compte de l’état et de la progression des actions en cours d’exécution sur les appareils.
  
    ![Graphique du modèle de signalement de la progression et de l’état de la gestion des appareils][img-report_progress_pattern]

## <a name="next-steps"></a>Étapes suivantes
Les fonctionnalités, les modèles et les bibliothèques de code fournis par IoT Hub pour la gestion des appareils vous permettent de créer des applications IoT qui respectent les exigences d’opérateur IoT en entreprise dans chaque phase du cycle de vie de l’appareil.

Pour plus d’informations sur les fonctionnalités de gestion des appareils dans IoT Hub, consultez le didacticiel [Prise en main de la gestion des appareils][lnk-get-started].

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
[lnk-dps]: https://azure.microsoft.com/documentation/services/iot-dps
