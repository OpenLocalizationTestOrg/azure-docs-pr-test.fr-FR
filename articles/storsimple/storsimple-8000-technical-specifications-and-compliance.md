---
title: "les spécifications techniques aaaStorSimple | Documents Microsoft"
description: "Décrit les spécifications techniques hello et les informations de conformité des réglementations en vigueur pour les composants matériels hello StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 98fa3307e2a929551c74e8b3179bb0fb61c0ab53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-specifications-and-compliance-for-hello-storsimple-device"></a>Spécifications techniques et conformité de l’appareil StorSimple hello

## <a name="overview"></a>Vue d'ensemble

composants de matériels Hello de votre appareil Microsoft Azure StorSimple respectent toohello les spécifications techniques et les normes décrites dans cet article. les spécifications techniques Hello décrivent la capacité de stockage des modules de refroidissement (PCM), les lecteurs de disque, hello et boîtiers. les informations de compatibilité Hello couvrent des éléments tels que les normes internationales, sécurité et émissions et le câblage.

## <a name="power-and-cooling-module-specifications"></a>Caractéristiques du module d’alimentation et de refroidissement

l’appareil StorSimple Hello a deux 100-240 V double ventilateur, compatibles Modules de refroidissement (PCM). Cette configuration fournit une alimentation redondante. Si un module PCM tombe en panne, appareil de hello continue normalement toooperate sur hello autre module jusqu'à ce que hello échoué module est remplacé.

Hello boîtiers utilise un PCM de 580 W et le boîtier principal utilise un PCM de 764 W. Hello tableaux ci-après les spécifications techniques hello liste associées hello PCM.

| Caractéristique | PCM 580 W (EBOD) | PCM 764 W (principal) |
| --- | --- | --- |
| Puissance de sortie maximale |580 W |764 W |
| Fréquence |50/60 Hz |50/60 Hz |
| Sélection de la plage de tension |Détermination automatique : 90 à 264 V CA, 47/63 Hz |Détermination automatique : 90 à 264 V CA, 47/63 Hz |
| Courant d’appel maximal |20 A |20 A |
| Correction du facteur de puissance |> 95 % de la tension d’entrée nominale |> 95 % de la tension d’entrée nominale |
| Harmonique |Conforme à la norme EN61000-3-2 |Conforme à la norme EN61000-3-2 |
| Sortie |Tension en mode veille 5 V @ 2,0 A |Tension en mode veille 5 V @ 2,7 A |
| +5 V @ 42 A |+5 V @ 40 A | |
| +12 V @ 38 A |+12 V @ 38 A | |
| Enfichable à chaud |Oui |Oui |
| Commutateurs et voyants LED |Interrupteur marche/arrêt et quatre voyants LED d’état |Interrupteur marche/arrêt et six voyants LED d’état |
| Refroidissement du boîtier |Ventilateurs axiaux avec vitesse variable réglable |Ventilateurs axiaux avec vitesse variable réglable |

## <a name="power-consumption-statistics"></a>Statistiques sur la consommation énergétique

Hello tableau suivant répertorie des données de consommation de puissance classique de hello (les valeurs réelles peuvent varier de hello publiée) pour hello divers modèles d’appareil StorSimple.

| Conditions | 240 V CA | 240 V CA | 240 V CA | 110 V CA | 110 V CA | 110 V CA |
| --- | --- | --- | --- | --- | --- | --- |
|  Ventilateurs lents, lecteurs inactifs |1,45 A |0,31 kW |1 057,76 BTU/heure |3,19 A |0,34 kW |1 160,13 BTU/heure |
|  Ventilateurs lents, lecteurs en cours d’accès |1,54 A |0,33 kW |1 126,01 BTU/heure |3,27 A |0,36 kW |1 228,37 BTU/heure |
|  Ventilateurs rapides, lecteurs inactifs, deux blocs d’alimentation sous tension |2,14 A |0,49 kW |1 671,95 BTU/heure |4,99 A |0,54 kW |1 842,56 BTU/heure |
|  Ventilateurs rapides, lecteurs inactifs, un bloc d’alimentation sous tension, un inactif |2,05 A |0,48 kW |1 637,83 BTU/heure |4,58 A |0,50 kW |1 706,07 BTU/heure |
|  Ventilateurs rapides, lecteurs en cours d’accès, deux blocs d’alimentation sous tension |2,26 A |0,51 kW |1 740,19 BTU/heure |4,95 A |0,54 kW |1 842,56 BTU/heure |
|  Ventilateurs rapides, lecteurs en cours d’accès, un bloc d’alimentation sous tension, un inactif |2,14 A |0,49 kW |1 671,95 BTU/heure |4,81 A |0,53 kW |1 808,44 BTU/heure |

## <a name="disk-drive-specifications"></a>Caractéristiques des lecteurs de disque

Votre appareil StorSimple prend en charge des lecteurs de disque SCSI SAS (Serial Attached) too12 format 3,5 pouces facteur. les disques réels Hello peuvent être un mélange de disques SSD (SSD) ou les lecteurs de disque dur (HDD), en fonction de la configuration du produit hello. emplacements de Hello 12 disques se trouvent dans une configuration de 3 par 4 devant boîtier de hello. permet de Hello boîtiers de stockage supplémentaire pour un autre 12 lecteurs de disque. Il s’agit toujours de disques durs.

## <a name="storage-specifications"></a>Spécifications de stockage

les appareils StorSimple Hello ont une combinaison de disques durs et des disques SSD pour les deux hello 8100 et 8600. la capacité totale utilisable Hello pour hello 8100 et 8600 sont à peu près 15 et 38 To respectivement. Hello tableau suivant décrit les détails hello SSD, disque dur et la capacité du cloud dans le contexte hello Hello capacité de la solution StorSimple.

| Modèle d’appareil/capacité | 8100 | 8600 |
| --- | --- | --- |
| Nombre de disques durs |8 |19 |
| Nombre de disques SSD |4 |5 |
| Capacité de disque dur unique |4 To |4 To |
| Capacité de disque SSD unique |400 Go |800 Go |
| Capacité de rechange |4 To |4 To |
| Capacité utilisable de disque dur |14 To |36 To |
| Capacité utilisable de disque SSD |800 Go |2 To |
| Capacité utilisable totale* |~ 15 To |~ 38 To |
| Capacité totale de la solution (y compris le cloud) |200 To |500 To |

<sup>* </sup>- *capacité totale Hello inclut hello la capacité disponible pour les données, les métadonnées et les mémoires tampons.*

## <a name="enclosure-dimensions-and-weight-specifications"></a>Dimensions et poids des boîtiers

suivant la liste des tables de Hello hello différentes spécifications de boîtier pour les dimensions et poids.

### <a name="enclosure-dimensions"></a>Dimensions de boîtier

Hello tableau suivant répertorie les dimensions hello du boîtier hello en millimètres et en pouces.

| Boîtier | Millimètres | Pouces |
| --- | --- | --- |
| Hauteur |87,9 |3,46 |
| Largeur entre brides de montage |483 |19,02 |
| Largeur du boîtier |443 |17,44 |
| Profondeur de tooextremity bride de montage du corps du boîtier |577 |22,72 |
| Profondeur des opérations du panneau toofurthest et l’extrémité du boîtier |630,5 |24,82 |
| Profondeur de monter la bride toofurthest et l’extrémité du boîtier |603 |23,74 |

### <a name="enclosure-weight"></a>Poids du boîtier

Selon la configuration de hello, un boîtier principal entièrement chargé peut peser entre 21 too33 kg et nécessite deux personnes toohandle il.

| Boîtier | Poids |
| --- | --- |
| Poids maximal (dépend de la configuration de hello) |30 à 33 kg |
| Vide (aucun disque monté) |21 à 23 kg |

## <a name="enclosure-environment-specifications"></a>Caractéristiques ambiantes pour le boîtier

Cette section répertorie l’environnement du boîtier hello spécifications toohello connexes. température de Hello, humidité, altitude, résistance aux chocs, vibration, orientation, sécurité et compatibilité électromagnétique (EMC) sont inclus dans cette catégorie.

### <a name="temperature-and-humidity"></a>Température et humidité

| Boîtier | Plage de températures ambiantes | Taux d’humidité ambiante | Température maximale du thermomètre mouillé |
| --- | --- | --- | --- |
| En fonctionnement |5 °C à 35 °C (41 °F à 95 °F) |20 à 80 % sans condensation |28 °C (82 °F) |
| Hors fonctionnement |-40 °C à 70 °C (40 °F à 158 °F) |5 à 100 % sans condensation |29 °C (84 °F) |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>Ventilation, altitude, chocs, vibrations, orientation, sécurité et CEM

| Boîtier | Caractéristiques en fonctionnement |
| --- | --- |
| Ventilation |Ventilation du système se toorear avant. Le système doit être utilisé avec une installation basse pression à échappement vers l’arrière. La contre-pression créée par les portes de rack et les obstacles ne doit pas dépasser 5 pascals (0,5 mm de colonne d’eau). |
| Altitude, en fonctionnement |-30 mètres too3045 mètres (too10-100 pieds, 000 pieds) avec une température maximale détarée de 5 ° C au-dessus de pieds 7000. |
| Altitude, hors fonctionnement |-305 mètres too12, 192 mètres (too40-1,000 pieds, 000 pieds) |
| Chocs, en fonctionnement |5 g 10 ms ½ sinus |
| Chocs, hors fonctionnement |30 g 10 ms ½ sinus |
| Vibrations, en fonctionnement |Moyenne quadratique 0,21 g, 5-500 Hz aléatoire |
| Vibrations, hors fonctionnement |Moyenne quadratique 1,04 g, 2-200 Hz aléatoire |
| Vibrations, déplacement |3 g 2-200 Hz sinus |
| Orientation et montage |Montage en rack de 19" (2 unités EIA) |
| Rails de rack |rayon de profondeur minimale de 700 mm (31.50 pouces) toofit conforme à la norme IEC 297 |
| Sécurité et homologations |CE et UL EN 61000-3, CEI 61000-3, UL 61000-3 |
| CEM |EN55022 (CISPR - A), FCC A |

## <a name="international-standards-compliance"></a>Conformité aux normes internationales

Votre appareil Microsoft Azure StorSimple est conforme à la suite de normes internationales de hello :  

* CE - EN 60950-1
* TooIEC de rapport CB 60950-1
* UL et cUL tooUL 60950-1

## <a name="safety-compliance"></a>Conformité aux normes de sécurité

Votre appareil Microsoft Azure StorSimple répond aux hello suit les normes de sécurité :

* Homologation du type de produit du système : UL, cUL, CE
* Conformité aux normes de sécurité : UL 60950, CEI 60950, EN 60950

## <a name="emc-compliance"></a>Conformité électromagnétique

Votre appareil Microsoft Azure StorSimple répond aux hello suivant les évaluations EMC.

### <a name="emissions"></a>Émissions

Appareil de Hello est EMC conforme pour les niveaux des émissions conduction et par rayonnement.

* Niveaux maximums d’émissions par conduction : CFR 47 partie 15 classe A, EN55022 classe A, CISPR classe A
* Niveaux maximums d’émissions par rayonnement : CFR 47 partie 15B classe A, EN55022 classe A, CISPR classe A

### <a name="harmonics-and-flicker"></a>Harmonique et papillotement

Appareil de Hello est conforme à la norme EN61000-3-2/3.

### <a name="immunity-limit-levels"></a>Niveaux maximums d’immunité

Appareil de Hello est conforme à la norme EN55024.

## <a name="ac-power-cord-compliance"></a>Conformité du cordon d’alimentation secteur

Hello plug- and hello complète cordon d’alimentation doit respecter les normes hello pour pays hello dans le hello périphérique est utilisé, et elles doivent avoir des autorisations de sécurité qui sont acceptables dans ce pays. les tables suivantes de Hello normes de liste pour l’Europe et des États-Unis de hello.

### <a name="ac-power-cords---usa-must-be-nrtl-listed"></a>Cordons d’alimentation secteur - États-Unis (doivent être répertoriés par un laboratoire d’essai reconnu nationalement)

| Composant | Caractéristique |
| --- | --- |
| Type de cordon |SV ou SVT, 18 AWG minimum, 3 conducteurs, longueur maximale 2 mètres |
| Fiche |Fiche avec mise à la terre NEMA 5-15P, avec une tension nominale de  120 V, 10 A ; ou CEI 320 C14, 250 V, 10 A |
| Prise |CEI 320 C-13, 250 V, 10 A |

### <a name="ac-power-cords---europe"></a>Cordons d’alimentation secteur - Europe

| Composant | Caractéristique |
| --- | --- |
| Type de cordon |Harmonisé, H05-VVF-3G1.0 |
| Prise |CEI 320 C-13, 250 V, 10 A |

## <a name="supported-network-cables"></a>Câbles réseau pris en charge

Pour les interfaces réseau hello 10 GbE, DATA 2 et 3 de données, consultez toohello [liste des câbles réseau pris en charge et des modules](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).

## <a name="next-steps"></a>Étapes suivantes

Vous êtes maintenant prêt toodeploy un appareil StorSimple dans votre centre de données. Pour plus d’informations, consultez [Déploiement de votre appareil local](storsimple-8000-deployment-walkthrough-u2.md).

