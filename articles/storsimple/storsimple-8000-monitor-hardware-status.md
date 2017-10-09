---
title: "aaaStorSimple 8000 composants matériels de série et l’état | Documents Microsoft"
description: "Découvrez comment toomonitor hello composants matériels de votre unité StorSimple via le service de gestionnaire de périphériques StorSimple hello."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 85b398e4b1a6b8921792b8945331325940082eb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-hardware-components-and-status"></a>Utiliser des composants matériels de hello le Gestionnaire de périphériques StorSimple service toomonitor et l’état
## <a name="overview"></a>Vue d'ensemble
Cet article décrit hello divers composants physiques et logiques de votre appareil de série StorSimple 8000 localement. Elle explique également comment toomonitor hello état du périphérique à l’aide de hello **contrôle d’intégrité de l’état et le matériel** panneau Bonjour service du Gestionnaire de périphériques StorSimple.

Hello **contrôle d’intégrité de l’état et le matériel** panneau affiche l’état du matériel de tous les composants de périphérique StorSimple hello hello.

Sous la liste des composants pour 8100 de hello, il existe trois sections décrivent :

* **Composants partagés** : ils ne font pas partie des contrôleurs de hello, telles que les lecteurs de disque, boîtier, les composants PCM et température, tension, capteurs et ligne actuelles.
* **Composants du contrôleur 0** – composants hello qui résident sur le contrôleur 0, tels que le contrôleur, expandeur SAS et le connecteur, les capteurs de température du contrôleur et hello différentes des interfaces réseau.
* **Composants du contrôleur 1** : hello des composants qui constituent le contrôleur 1, similaires toothose détaillé pour le contrôleur 0.

Un appareil 8600 a des composants supplémentaires qui correspondent toohello ensemble de disques boîtier EBOD (Extended). Sous la liste des composants de hello, il existe cinq sections. Parmi ceux-ci, il existe trois sections qui contiennent des composants hello dans le boîtier principal de hello et toohello identiques celles décrites pour 8100. Il existe deux sections supplémentaires pour hello boîtiers qui décrivent :

* **Les composants du contrôleur EBOD 0** – hello composants qui résident sur le boîtier EBOD 0, tels que le contrôleur EBOD hello, capteurs de température expander et connecteur et contrôleur SAS.
* **Composants du contrôleur 1 EBOD** – hello des composants qui constituent le boîtier EBOD 1, toothose similaire détaillés pour le boîtier EBOD 0.
* **Composants partagés du boîtier EBOD** : composants de hello présents dans les boîtiers hello et PCM qui ne font pas partie du contrôleur EBOD de hello.

> [!NOTE]
> **état du matériel Hello n’est pas disponible pour un dispositif de Cloud StorSimple (8010/8020).**


## <a name="monitor-hello-hardware-status"></a>Surveiller l’état du matériel hello
Effectuez hello suivant l’état du matériel étapes tooview hello d’un composant de l’appareil :

1. Accédez trop**périphériques**, sélectionnez un périphérique StorSimple spécifique. Accédez trop**analyse > état du matériel**.

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health1.png)

2. Recherchez hello **composants matériels** section et choisissez parmi les composants disponibles hello. Simplement sur hello composant étiquette tooexpand hello liste et afficher l’état de hello Hello différents composants de l’appareil. Consultez hello [liste de composant détaillé pour le boîtier principal de hello](#component-list-for-primary-enclosure-of-storsimple-device) et hello [liste de composant détaillé pour hello boîtiers](#component-list-for-ebod-enclosure-of-storsimple-device).

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health2.png)

3. Hello suivant l’état du composant hello toointerpret du schéma de codage en couleurs, utilisez :
   
   * **Coche verte** – Composant sain à l’état **OK**.
   * **Jaune** – Composant défectueux à l’état **Avertissement**.
   * **Point d’exclamation rouge** – Composant à l’état **Échec**.
   * **Blanc avec texte noir** – Composant absent.
   
   Hello capture d’écran suivante montre un appareil disposant de composants dans **OK**, **avertissement**, et **échec** état.
       
   ![](./media/storsimple-8000-monitor-hardware-status/hw-health3.png)

   Expansion hello **liste de composants partagés**, nous pouvons voir cluster hello NVRAM et hello sont détériorés.

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health5.png)

   Expansion hello **composants du contrôleur 1** liste, nous pouvons voir ce nœud de cluster hello a échoué.  

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health4.png)  

4. Si vous rencontrez un composant dont l'état n'est pas **sain** , contactez le Support technique de Microsoft. Si les alertes sont activées sur votre appareil, vous recevrez un message d'alerte. Si vous avez besoin d’un composant matériel défaillant de tooreplace, consultez [remplacement de composant matériel StorSimple](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>Liste des composants du boîtier principal de l'appareil StorSimple
Hello tableau suivant indique hello composants physiques et logiques contenus dans le boîtier principal et hello (présent dans 8100 et 8600) de l’appareil StorSimple local.

| Composant | Module | Type | Lieu | Unité remplaçable sur site (FRU) ? | Description |
| --- | --- | --- | --- | --- | --- |
| Lecteur à l’emplacement [0-11] |Lecteurs de disque |Physique |Partagé |Oui |Une ligne est présentée pour chacun des hello SSD ou hello HDD disques dans le boîtier principal de hello. |
| Capteur de température ambiante |Boîtier |Physique |Partagé |Non |Mesures hello température dans le châssis de hello. |
| Capteur de température du plan médian |Boîtier |Physique |Partagé |Non |Mesures hello température de plan hello. |
| Alarme sonore |Boîtier |Physique |Partagé |Non |Indique si le sous-système d’alarme hello dans le châssis de hello est fonctionnel. |
| Boîtier |Boîtier |Physique |Partagé |Oui |Indique la présence de hello d’un châssis. |
| Paramètres du boîtier |Boîtier |Physique |Partagé |Non |Fait référence toohello le panneau avant du châssis de hello. |
| Capteurs de tension de ligne |PCM |Physique |Partagé |Non |Nombreux capteurs de tension de ligne l’état sont affiché, ce qui indique si hello mesurée tension est au sein de la tolérance de panne. |
| Capteurs de courant de ligne |PCM |Physique |Partagé |Non |Nombreux capteurs de courant l’état sont affiché, ce qui indique si hello courant mesuré est dans la tolérance de panne. |
| Capteurs de température dans PCM |PCM |Physique |Partagé |Non |Nombreux capteurs de température telles que les capteurs d’entrée et de la zone réactive l’état sont affiché, indiquant si hello mesurée température se trouve dans la tolérance de panne. |
| Alimentation électrique [0-1] |PCM |Physique |Partagé |Oui |Une ligne est présentée pour chacun des blocs d’alimentation hello hello deux PCM situés dans hello arrière appareil de hello. |
| Refroidissement [0-1] |PCM |Physique |Partagé |Oui |Une ligne est présentée pour chacun des hello quatre ventilateurs résidant dans hello deux PCM. |
| Batterie [0-1] |PCM |Physique |Partagé |Oui |Une ligne est présentée pour chaque module de batterie de secours hello qui est insérées dans hello PCM. |
| Metis |N/A |Opérateurs logiques |Partagé |N/A |Indique l’état de hello de batteries de hello : si ils ont besoin de charge et que vous rapprochez de fin de vie. |
| Cluster |N/A |Opérateurs logiques |Partagé |N/A |Affiche hello état du cluster de hello qui est créé entre les deux modules de contrôleur intégrés hello. |
| Nœud de cluster |N/A |Opérateurs logiques |Partagé |N/A |Indique l’état hello du contrôleur hello en tant que partie du cluster de hello. |
| Quorum du cluster |N/A |Opérateurs logiques | |N/A |Indique la présence de hello d’appartenance de disque majoritaire hello Bonjour pool de stockage de disque dur. |
| Espace de données du disque dur |N/A |Opérateurs logiques |Partagé |N/A |espace de stockage Hello qui est utilisé pour les données dans le pool de stockage de disque dur (HDD) hello. |
| Espace de gestion du disque dur |N/A |Opérateurs logiques |Partagé |N/A |Hello un espace réservé dans hello pool de stockage de disque dur pour les tâches de gestion. |
| Espace du quorum du disque dur |N/A |Opérateurs logiques |Partagé |N/A |Hello un espace réservé dans hello pool de stockage de disque dur pour le quorum de cluster. |
| Espace de remplacement du disque dur |N/A |Opérateurs logiques |Partagé |N/A |Hello un espace réservé dans hello pool de stockage de disque dur pour le remplacement du contrôleur. |
| Espace de données SSD |N/A |Opérateurs logiques |Partagé |N/A |espace de stockage Hello utilisé pour les données dans le pool de stockage hello solid state Drive drive (SSD). |
| Espace NVRAM SSD |N/A |Opérateurs logiques |Partagé |N/A |espace de stockage Hello Bonjour pool de stockage SSD dédié pour la logique de la mémoire NVRAM. |
| Pool de stockage du disque dur |N/A |Opérateurs logiques |Partagé |N/A |Affiche hello état hello logique du pool de stockage qui est créé à partir de disques durs de périphérique. |
| Pool de stockage SSD |N/A |Opérateurs logiques |Partagé |N/A |Affiche hello état hello logique du pool de stockage qui est créé à partir de disques SSD d’appareil. |
| Contrôleur [0-1] [état] |E/S |Physique |Controller |Oui |Indique l’état de hello hello du contrôleur de, et s’il est en mode actif ou veille dans le châssis de hello. |
| Capteurs de température du contrôleur |E/S |Physique |Controller |Non |Nombreux capteurs de température telles que le module d’e/s, de température de l’UC, DIMM et PCIe l’état sont affiché, qui indique si est ou non température hello rencontré au sein de la tolérance de panne. |
| Expander SAS |E/S |Physique |Controller |Non |Indique hello du hello série attaché SCSI (SAS) expander, qui est utilisé tooconnect hello stockage intégré toohello contrôleur. |
| Connecteur SAS [0-1] |E/S |Physique |Controller |Non |Indique l’état hello de chaque connecteur SAS, qui est utilisé tooconnect intégré stockage toohello SAS expander. |
| Interconnexion de plan médian SBB |E/S |Physique |Controller |Non |Indique hello du connecteur de plan hello, qui est utilisé tooconnect chaque plan toohello contrôleur. |
| Cœur de processeur |E/S |Physique |Controller |Non |Indique l’état hello hello de cœurs de processeur dans chaque contrôleur. |
| Puissance électronique du boîtier |E/S |Physique |Controller |Non |Indique l’état de hello hello système d’alimentation utilisé par boîtier de hello. |
| Diagnostic électronique du boîtier |E/S |Physique |Controller |Non |Indique l’état hello des sous-systèmes de diagnostic hello fourni par le contrôleur de hello. |
| Baseboard Management Controller (BMC) |E/S |Physique |Controller |Non |Indique l’état de hello de hello baseboard management controller (BMC), qui est un processeur de service spécialisé qui surveille le périphérique hello via les capteurs et communique avec l’administrateur du système hello via une connexion indépendante. |
| Ethernet |E/S |Physique |Controller |Non |Indique l’état de hello de chacune des interfaces réseau de hello, autrement dit, gestion de hello et les ports de données fournis sur le contrôleur de hello. |
| NVRAM |E/S |Physique |Controller |Non |Indique l’état hello de la mémoire NVRAM, une mémoire vive non volatile avec batterie de secours hello qui remplit les tooretain des informations critiques de l’application dans l’événement hello de panne de courant. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>Liste des composants du boîtier EBOD de l'appareil StorSimple
Hello tableau suivant indique hello composants physiques et logiques contenus dans hello boîtiers (uniquement présentes dans le modèle 8600) de l’appareil StorSimple local.

| Composant | Module | Type | Lieu | FRU ? | Description |
| --- | --- | --- | --- | --- | --- |
| Lecteur à l’emplacement [0-11] |Lecteurs de disque |Physique |Partagé |Oui |Une ligne est présentée pour chacun des lecteurs de disque dur devant hello hello boîtiers de hello. |
| Capteur de température ambiante |Boîtier |Physique |Partagé |Non |Mesures hello température dans le châssis de hello. |
| Capteur de température du plan médian |Boîtier |Physique |Partagé |Non |Mesures hello température de plan hello. |
| Alarme sonore |Boîtier |Physique |Partagé |Non |Indique si le sous-système d’alarme hello dans le châssis de hello est fonctionnel. |
| Boîtier |Boîtier |Physique |Partagé |Oui |Indique la présence de hello d’un châssis. |
| Paramètres du boîtier |Boîtier |Physique |Partagé |Non |Fait référence toohello OPS ou un hello le panneau avant du châssis de hello. |
| Capteurs de tension de ligne |PCM |Physique |Partagé |Non |Nombreux capteurs de tension de ligne l’état sont affiché, ce qui indique si hello mesurée tension est au sein de la tolérance de panne. |
| Capteurs de courant de ligne |PCM |Physique |Partagé |Non |Nombreux capteurs de courant l’état sont affiché, ce qui indique si hello courant mesuré est dans la tolérance de panne. |
| Capteurs de température dans PCM |PCM |Physique |Partagé |Non |Nombreux capteurs de température telles que les capteurs d’entrée et de la zone réactive l’état sont affiché, ce qui indique si hello mesurée température se trouve dans la tolérance de panne. |
| Alimentation électrique [0-1] |PCM |Physique |Partagé |Oui |Une ligne est présentée pour chacun des blocs d’alimentation hello hello deux PCM situés dans hello arrière appareil de hello. |
| Refroidissement [0-1] |PCM |Physique |Partagé |Oui |Une ligne est présentée pour chacun des hello quatre ventilateurs résidant dans hello deux PCM. |
| Stockage local [HDD] |N/A |Opérateurs logiques |Partagé |N/A |Affiche hello état hello logique du pool de stockage qui est créé à partir de disques durs de périphérique. |
| Contrôleur [0-1] [état] |E/S |Physique |Controller |Oui |Affiche hello état des contrôleurs hello dans le module EBOD de hello. |
| Capteurs de température dans EBOD |E/S |Physique |Controller |Non |Nombreux capteurs de température de chaque contrôleur de l’état sont affiché, qui indique si la température hello rencontrée est dans la tolérance de panne. |
| Expander SAS |E/S |Physique |Controller |Non |Indique l’état hello de l’expandeur SAS hello, qui est utilisé tooconnect hello stockage intégré toohello contrôleur. |
| Connecteur SAS [0-2] |E/S |Physique |Controller |Non |Indique l’état hello de chaque connecteur SAS, qui est utilisé tooconnect intégré stockage toohello SAS expander. |
| Interconnexion de plan médian SBB |E/S |Physique |Controller |Non |Indique hello du connecteur de plan hello, qui est utilisé tooconnect chaque plan toohello contrôleur. |
| Puissance électronique du boîtier |E/S |Physique |Controller |Non |Indique l’état de hello hello système d’alimentation utilisé par boîtier de hello. |
| Diagnostic électronique du boîtier |E/S |Physique |Controller |Non |Indique l’état hello des sous-systèmes de diagnostic hello fourni par le contrôleur de hello. |
| Contrôleur toodevice de connexion |E/S |Physique |Controller |Non |Indique l’état hello de connexion hello entre le module d’e/s EBOD hello et contrôleur de l’appareil hello. |

## <a name="next-steps"></a>Étapes suivantes
* toouse hello, le Gestionnaire de périphériques StorSimple service tooadminister votre appareil, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).
* Si vous avez besoin de tootroubleshoot un composant de périphérique qui a l’état détérioré ou en échec, consultez trop[StorSimple indicateurs de surveillance](storsimple-monitoring-indicators.md).
* tooreplace un composant matériel défaillant, consultez [remplacement de composant matériel StorSimple](storsimple-hardware-component-replacement.md).
* Si vous continuez de problèmes de l’appareil tooexperience, [contactez le Support Microsoft](storsimple-8000-contact-microsoft-support.md).

