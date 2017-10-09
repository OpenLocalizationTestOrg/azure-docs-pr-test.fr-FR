---
title: gestion des aaaDevice avec Azure IoT Hub | Documents Microsoft
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
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>Vue d’ensemble de la gestion des appareils avec IoT Hub
## <a name="introduction"></a>Introduction
IoT Hub Azure fournit les fonctions hello et un modèle d’extensibilité qui permettent aux périphériques et solutions de gestion de périphérique robuste toobuild principaux développeurs. Appareils comprise capteurs contraints et Microcontrôleurs de fonction unique, passerelles toopowerful qui acheminent des communications pour les groupes de périphériques.  En outre, les cas d’usage hello et configuration requise pour les opérateurs IoT considérablement varie secteurs.  En dépit de cette variante, gestion des appareils avec IoT Hub fournit le code bibliothèques toocater tooa ensemble diversifié d’appareils et les utilisateurs finaux, les modèles et les fonctionnalités de hello.

Une partie essentielle de la création d’une solution IoT réussie est tooprovide une stratégie pour comment opérateurs gérer hello en cours de leur collection de périphériques. Les opérateurs IoT nécessitent fiables et simples des outils et les applications qui les activer toofocus sur hello plusieurs aspects stratégiques de leur travail. Cet article fournit :

* Une vue d’ensemble de la gestion de toodevice approche Azure IoT Hub.
* Une description des principes courants de gestion des appareils.
* Description du cycle de vie de périphérique hello.
* Une vue d’ensemble des modèles courants de gestion des appareils.

## <a name="device-management-principles"></a>Principes de gestion des appareils
IoT offre un ensemble de défis de gestion d’appareil unique, et chaque solution d’entreprise doit résoudre hello suivant des principes :

![Graphique Principes de gestion des appareils][img-dm_principles]

* **Mise à l’échelle et automatisation**: IoT solutions nécessitent des outils simples qui automatisent les tâches de routine et l’activation d’une opération relativement faible du personnel toomanage des millions d’appareils. Quotidiennes, les opérateurs estiment toohandle les opérations de périphérique à distance, en bloc, et tooonly être averti lorsque des problèmes surviennent qui nécessitent leur attention directe.
* **Ouverture et compatibilité**: écosystème de périphériques hello est extrêmement divers. Outils de gestion doivent être adapté tooaccommodate une multitude de protocoles, les plateformes et les classes de périphériques. Les opérateurs doivent être en mesure de toosupport plus contraint de nombreux types d’appareils, à partir de hello incorporé chips de processus unique, toopowerful et ordinateurs entièrement fonctionnelles.
* **Prise en compte du contexte** : les environnements IoT sont dynamiques et en perpétuelle évolution. La fiabilité du service est primordiale. Les opérations de gestion de périphérique doivent tenir hello compte suivant facteurs tooensure maintenance temps d’arrêt n’affectent des opérations critiques ou créer des conditions dangereuses :
    * Fenêtres de maintenance SLA
    * États du réseau et de l’alimentation
    * Conditions d’utilisation
    * Géolocalisation des appareils
* **De nombreux rôles de service**: prise en charge pour les processus IoT des rôles d’opérations et de flux de travail unique hello est essentiel. personnel chargé des opérations Hello doit fonctionnent en harmonie avec hello des contraintes de services informatiques internes.  Il doivent également trouver des façons durable toosurface en temps réel appareil opérations informations toosupervisors et autres rôles de gestion d’entreprise.

## <a name="device-lifecycle"></a>Cycle de vie des appareils
Il existe un ensemble d’étapes de gestion générale des appareils qui sont des projets de IoT entreprise tooall courants. Dans Azure IoT, il existe cinq étapes au sein du cycle de vie hello appareil :

![Hello cinq phases de cycle de vie des appareils Azure IoT : planifier, de configurer, de configurer, de surveiller, de mettre hors service][img-device_lifecycle]

Dans chacun de ces cinq étapes, il existe plusieurs conditions d’opérateur de périphérique qui doivent être remplie tooprovide une solution complète :

* **Plan**: activer les opérateurs toocreate un schéma de métadonnées de périphérique qui leur permet de tooeasily et précisément la requête et cibler un groupe de périphériques pour les opérations de gestion en bloc. Vous pouvez utiliser hello appareil double toostore ces métadonnées de l’appareil sous forme de hello d’étiquettes et les propriétés.
  
    *Informations supplémentaires*: [prise en main jumeaux de périphérique][lnk-twins-getstarted], [comprendre jumeaux de périphérique][lnk-twins-devguide], [comment Propriétés du double périphérique toouse][lnk-twin-properties].
* **Disposition**: configurer en toute sécurité les nouveaux appareils tooIoT Hub et activer les opérateurs tooimmediately découvrir les fonctionnalités de l’appareil.  Utilisez hello IoT Hub identité Registre toocreate DISPOSITIF flexible des identités et des informations d’identification et effectuer cette opération en bloc à l’aide d’un travail. Générer des périphériques tooreport leurs capacités et les conditions via les propriétés du périphérique en double d’appareil hello.
  
    *Informations supplémentaires*: [gérer les identités d’appareil][lnk-identity-registry], [en bloc de gestion des identités d’appareil][lnk-bulk-identity], [Comment toouse appareil à deux propriétés][lnk-twin-properties].
* **Configurer**: faciliter en bloc les modifications de configuration et de microprogramme met à jour toodevices tout en conservant l’intégrité et la sécurité. Effectuez ces opérations de gestion d’appareils en bloc à l’aide des propriétés requises ou de méthodes directes et de travaux de diffusion.
  
    *Informations supplémentaires*: [utiliser les méthodes directes][lnk-c2d-methods], [appeler une méthode directe sur un appareil][lnk-methods-devguide], [comment Propriétés du double périphérique toouse][lnk-twin-properties], [planification et les tâches de diffusion][lnk-jobs], [planifier des travaux sur plusieurs appareils] [lnk-jobs-devguide].
* **Moniteur**: surveiller le contrôle d’intégrité de la collection globale de périphérique, état hello des opérations en cours et tooissues d’avertir les utilisateurs qui peuvent nécessiter une attention particulière.  Appliquer hello appareil double tooallow périphériques tooreport en temps réel des conditions de fonctionnement et l’état des opérations de mise à jour. Problèmes de génération des rapports de tableau de bord performant que hello surface urgentes à l’aide de requêtes de double de périphérique.
  
    *Informations supplémentaires*: [comment toouse appareil à deux propriétés][lnk-twin-properties], [langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages] [ lnk-query-language].
* **Mettre hors service**: remplacer ou mettre hors service des appareils après une défaillance, cycle, de mise à niveau ou à fin hello de durée de vie de service hello.  Utiliser les informations de périphérique de hello appareil double toomaintain si l’appareil physique de hello est en cours de remplacé ou archivé si en cours de mise hors service. Utilisez hello Registre des identités IoT Hub pour la révocation en toute sécurité les informations d’identification et les identités des appareils.
  
    *Informations supplémentaires*: [comment toouse appareil à deux propriétés][lnk-twin-properties], [gérer les identités d’appareil][lnk-identity-registry].

## <a name="device-management-patterns"></a>Modèle de gestion des appareils
IoT Hub permet hello suivant l’ensemble de modèles de gestion des appareils.  Hello [didacticiels de gestion de périphérique] [ lnk-get-started] indiquent en détail comment tooextend ces toofit modèles votre scénario et comment toodesign nouveaux modèles basés sur ces modèles de base.

* **Redémarrez** -hello principal application informe les appareil hello via une méthode directe qu’il a lancé un redémarrage.  Hello périphérique utilise hello a signalé l’état propriétés tooupdate hello redémarrage appareil de hello.
  
    ![Graphique du modèle de redémarrage de la gestion des appareils][img-reboot_pattern]
* **Paramètres d’usine** -hello principal application informe les appareil hello via une méthode directe qu’il a lancé une réinitialisation des paramètres.  Hello périphérique utilise hello signalé propriétés tooupdate hello réinitialisation état du périphérique de hello.
  
    ![Graphique du modèle de réinitialisation aux paramètres d’usine de la gestion des appareils][img-facreset_pattern]
* **Configuration** -hello principal application utilise des logiciels de tooconfigure de propriétés hello souhaitée en cours d’exécution sur l’appareil de hello.  Hello périphérique utilise hello signalé aucun état de configuration de tooupdate de propriétés du périphérique de hello.
  
    ![Graphique du modèle de configuration de la gestion des appareils][img-config_pattern]
* **Mise à jour de microprogramme** -hello principal application informe les appareil hello via une méthode directe qu’il a lancé une mise à jour du microprogramme.  périphérique de Hello établit une image de microprogramme de processus en plusieurs étapes toodownload hello, appliquer l’image de microprogramme hello et enfin vous reconnecter toohello IoT Hub service.  Tout au long du processus en plusieurs étapes hello, hello périphérique utilise hello signalé progression de propriétés tooupdate hello et l’état de l’appareil de hello.
  
    ![Graphique du modèle de mise à jour du microprogramme de la gestion des appareils][img-fwupdate_pattern]
* **Signaler la progression et l’état** -hello solution back-end exécute des requêtes de double de périphérique, sur un ensemble de périphériques, tooreport sur l’état de hello et la progression des actions en cours d’exécution sur les appareils hello.
  
    ![Graphique du modèle de signalement de la progression et de l’état de la gestion des appareils][img-report_progress_pattern]

## <a name="next-steps"></a>Étapes suivantes
les fonctions Hello, les modèles et les bibliothèques de code qui fournit des IoT Hub pour la gestion des appareils, vous permettent aux applications de IoT toocreate répondant aux besoins de l’opérateur IoT entreprise au sein de chaque étape du cycle de vie de périphérique.

toocontinue en savoir plus sur les fonctionnalités de gestion des appareils hello dans IoT Hub, consultez hello [prise en main la gestion des appareils] [ lnk-get-started] didacticiel.

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
