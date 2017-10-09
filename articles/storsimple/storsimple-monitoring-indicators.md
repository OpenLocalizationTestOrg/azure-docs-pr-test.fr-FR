---
title: "indicateurs de surveillance d’aaaStorSimple | Documents Microsoft"
description: "Décrit hello diodes électroluminescentes (DEL) et des alarmes sonores utilisés toomonitor hello état de l’appareil StorSimple hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Utiliser StorSimple toomanage des indicateurs de surveillance de votre appareil
## <a name="overview"></a>Vue d'ensemble
Votre appareil StorSimple comprend des diodes électroluminescentes (DEL) et les alertes que vous pouvez utiliser toomonitor hello modules et état global de l’appareil StorSimple hello. Vous trouverez Hello indicateurs de surveillance sur les composants matériels de hello du boîtier principal de l’appareil hello et boîtiers hello. Hello indicateurs de surveillance peut être DEL ou des alarmes sonores.

Il existe trois états tooindicate hello voyant d’un module : vert, orange-vert toored, clignotant ou rouge-orange.  

* Les LED vertes correspondent à un bon état de fonctionnement.  
* Toored-orange vert clignotant DEL représentent la présence de hello des conditions non critiques pouvant nécessiter l’intervention de l’utilisateur.  
* Les DEL rouge-orange indiquent qu’il y a une panne critique dans le module de hello.  

reste Hello de cet article décrit hello différentes LED témoins de surveillance, leur emplacement sur l’appareil StorSimple hello, état du périphérique hello selon hello des États de LED et les alarmes sonores associées.

## <a name="front-panel-indicator-leds"></a>Voyants LED du panneau avant
façade Hello, également appelé hello *panneau d’opérations* ou *panneau ops*, affiche l’état d’agrégation de tous les modules hello hello dans le système de hello. façade Hello est identique sur hello StorSimple principal et hello boîtiers et est illustrée ci-dessous.  

   ![Panneau avant de l’appareil][1]

façade Hello contient hello suivant indicateurs :  

1. Bouton Muet
2. Voyant LED d’alimentation (vert/rouge-orange)
3. Voyant LED de panne de module (ALLUMÉ rouge-orange/ÉTEINT)
4. Voyant LED d’erreur logique (ALLUMÉ rouge-orange/ÉTEINT)
5. Affichage de l’ID de l’unité  

différence majeure entre hello façade DEL pour appareil de hello et ceux pour hello boîtiers Hello est hello **numéro d’Identification système unité** affiché en hello DEL. unité par défaut de Hello affiché sur le périphérique de hello est **00**, alors que l’ID d’unité par défaut hello affiché sur hello boîtiers **01**. Cela vous permet de tooquickly différencier les appareil hello et boîtiers hello lorsque l’appareil de hello est activée. Si votre appareil est mis hors tension, utilisez les informations de hello fournies dans [activer un nouveau périphérique](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) périphérique hello toodifferentiate hello boîtiers.  

## <a name="front-panel-led-status"></a>État des LED du panneau avant
Utilisez hello suivant état hello tooidentify de la table indiquée par hello DEL du panneau avant de hello pour appareil de hello ou boîtiers hello.  

| Alimentation du système | Panne de module | Erreur logique | Alarme | État |
| --- | --- | --- | --- | --- |
| Rouge-orange |ÉTEINT |ÉTEINT |N/A |Alimentation secteur coupée, fonctionnement sur l’alimentation de secours ou alimentation secteur sur et modules de contrôleur hello ont été supprimés. |
| Vert |ACTIVÉ |ACTIVÉ |N/A |État de test panneau de commande à la mise sous tension (5 s) |
| Vert |ÉTEINT |ÉTEINT |N/A |Mise sous tension, tout fonctionne correctement |
| Vert |ACTIVÉ |N/A |LED de panne de PCM, LED de panne de ventilateur |Panne de PCM, panne de ventilateur, surchauffe ou température insuffisante |
| Vert |ACTIVÉ |N/A |LED de module d’E/S |Panne de module de contrôleur |
| Vert |ACTIVÉ |N/A |N/A |Erreur logique du boîtier |
| Vert |Clignote |N/A |LED d’état du module sur le module de contrôleur. LED de panne de PCM, LED de panne de ventilateur |Type de module de contrôleur installé inconnu, défaillance du bus I2C, erreur de configuration des données VPD (Vital Product Data) du module de contrôleur |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Voyants LED du module d’alimentation et de refroidissement (PCM)
Alimentation refroidissement (PCM) DEL témoins du module sont accessibles sur hello à l’arrière du boîtier principal de hello ou boîtiers de chaque module PCM. Cette rubrique explique comment hello toouse suivant l’état de hello toomonitor DEL de votre appareil StorSimple.  

* DEL du PCM du boîtier principal hello
* DEL du PCM pour hello boîtiers

## <a name="pcm-leds-for-hello-primary-enclosure"></a>DEL du PCM du boîtier principal hello
l’appareil StorSimple Hello a un module PCM de 764 w avec une batterie supplémentaire. Hello illustration suivante montre le panneau de DEL hello pour appareil de hello.  

   ![DEL du PCM sur le boîtier principal de hello][2]

Légende des LED :

1. Panne d’alimentation secteur
2. Panne de ventilateur
3. Panne de batterie
4. PCM OK
5. Panne d’alimentation CC
6. Batterie en bon état  

état Hello Hello que PCM est indiqué sur hello conduit le panneau de configuration. Panneau de DEL du PCM du périphérique Hello compte six DEL. Quatre de ces DEL afficher hello état d’alimentation hello et ventilateur de hello. Hello restant deux DEL indique l’état hello du module de batterie de secours hello Bonjour PCM. Vous pouvez utiliser hello suivant l’état de hello toodetermine tables Hello PCM.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>Voyants LED du PCM relatifs à l’alimentation et au ventilateur
| État | PCM OK (vert) | Panne d’alimentation secteur (orange) | Panne de ventilateur (orange) | Panne d’alimentation CC (orange) |
| --- | --- | --- | --- | --- |
| Aucune alimentation secteur (tooenclosure) |ÉTEINT |ÉTEINT |ÉTEINT |ÉTEINT |
| Absence d’alimentation secteur (ce PCM uniquement) |ÉTEINT |ACTIVÉ |ÉTEINT |ACTIVÉ |
| PCM alimenté sur secteur - OK |ACTIVÉ |ÉTEINT |ÉTEINT |ÉTEINT |
| Panne de PCM (panne de ventilateur) |ÉTEINT |ÉTEINT |ACTIVÉ |N/A |
| Panne de PCM (surampérage, surtension, surintensité) |ÉTEINT |ACTIVÉ |ACTIVÉ |ACTIVÉ |
| PCM (ventilateur hors tolérance) |ACTIVÉ |ÉTEINT |ÉTEINT |ACTIVÉ |
| Mode veille |Clignote |ÉTEINT |ÉTEINT |ÉTEINT |
| Téléchargement du microprogramme de PCM |ÉTEINT |Clignote |Clignote |Clignote |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>Pour une batterie de secours hello DEL témoins du PCM
| État | Batterie en bon état (vert) | Panne de batterie (orange) |
| --- | --- | --- |
| Batterie non présente |ÉTEINT |ÉTEINT |
| Batterie présente et chargée |ACTIVÉ |ÉTEINT |
| Batterie en charge ou décharge de maintenance |Clignote |ÉTEINT |
| Erreur logicielle de batterie (récupérable) |ÉTEINT |Clignote |
| Erreur matérielle de batterie (non récupérable) |ÉTEINT |ACTIVÉ |
| Batterie désamorcée |Clignote |ÉTEINT |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>DEL du PCM pour hello boîtiers
Hello boîtiers a un PCM de 580 w et sans batterie supplémentaire. panneau PCM Hello hello boîtiers a LED uniquement pour les alimentations hello et ventilateur de hello. Hello l’illustration suivante montre ces DEL.

   ![DEL du PCM sur hello boîtiers][3] 

Vous pouvez utiliser hello suivant l’état de hello toodetermine table Hello PCM.  

| État | PCM OK (vert) | Panne d’alimentation secteur (orange) | Panne de ventilateur (orange) | Panne d’alimentation CC (orange) |
| --- | --- | --- | --- | --- |
| Aucune alimentation secteur (tooenclosure) |ÉTEINT |ÉTEINT |ÉTEINT |ÉTEINT |
| Absence d’alimentation secteur (ce PCM uniquement) |ÉTEINT |ACTIVÉ |ÉTEINT |ACTIVÉ |
| PCM alimenté sur secteur - OK |ACTIVÉ |ÉTEINT |ÉTEINT |ÉTEINT |
| Panne de PCM (panne de ventilateur) |ÉTEINT |ÉTEINT |ACTIVÉ |X |
| Panne de PCM (surampérage, surtension, surintensité) |ÉTEINT |ACTIVÉ |ACTIVÉ |ACTIVÉ |
| PCM (ventilateur hors tolérance) |ACTIVÉ |ÉTEINT |ÉTEINT |ACTIVÉ |
| Mode veille |Clignote |ÉTEINT |ÉTEINT |ÉTEINT |
| Téléchargement du microprogramme de PCM |ÉTEINT |Clignote |Clignote |Clignote |

## <a name="controller-module-indicator-leds"></a>Voyants LED du module de contrôleur
l’appareil StorSimple Hello contient des DEL de contrôleur principal de hello et les modules de contrôleur EBOD hello.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>DEL de surveillance pour le contrôleur principal de hello
Hello l’illustration suivante permet d’identifier les DEL hello sur le contrôleur principal de hello. (Tous les composants de hello sont tooaid répertorié dans l’orientation.)  

   ![LED de surveillance - Contrôleur principal][4]

Utilisez hello suivant table toodetermine si le module de contrôleur hello fonctionne correctement.  

### <a name="controller-indicator-leds"></a>Voyants LED du contrôleur
| LED | Description |
| --- | --- |
| LED d’ID (bleue) |Indique que le module hello est identifié. Si hello DEL bleue clignote sur un contrôleur en cours d’exécution, puis hello contrôleur est hello contrôleur actif et hello autre est contrôleur de secours hello. Pour plus d’informations, consultez [contrôleur actif de hello identifier sur votre appareil](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| LED de panne (orange) |Indique une erreur dans le contrôleur de hello. |
| LED OK (verte) |Vert fixe indique que ce contrôleur hello est OK. Une LED verte clignotante indique une erreur de configuration de données VPD du contrôleur. |
| LED d’activité SAS (vertes) |Le vert fixe indique une connexion sans activité en cours. Vert clignotant indique la connexion de hello a une activité en cours. |
| LED d’état Ethernet |Le côté droit indique l’activité lien/réseau : (vert fixe) lien actif, (vert clignotant) activité réseau. Le côté gauche indique la vitesse du réseau: (jaune) 1 000 Mbits/s, (vert) 100 Mbits/s (vert) et (ÉTEINT) 10 Mbits/s. Selon le modèle de composant hello, ce voyant peut clignoter même si l’interface de réseau hello n’est pas activé. |
| LED POST |Indique la progression du démarrage hello lorsque la tension du contrôleur hello. Si l’appareil StorSimple hello échoue tooboot, cette DEL aide Support Microsoft identifier point hello dans le processus de démarrage hello auquel hello défaillance. |

> [!IMPORTANT]
> Si la DEL de défaillance hello est allumée, il est un problème avec le module de contrôleur hello pouvant être résolu en redémarrant le contrôleur de hello. Si le contrôleur de hello redémarrage ne résout pas ce problème, contactez le Support Microsoft.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>DEL de surveillance pour hello EBOD (boîtiers)
Chacun des hello 6 Go/contrôleurs SAS EBOD de s comportent des DEL qui indiquent leur état, comme indiqué dans hello après l’illustration.  

  ![LED de surveillance - Boîtier EBOD][5]

Utilisez hello suivant table toodetermine si le module de contrôleur EBOD hello fonctionne normalement.  

### <a name="ebod-controller-module-indicator-leds"></a>Voyants LED du module de contrôleur EBOD
| État | Module d’E/S OK (vert) | Panne du module d’E/S (orange) | Activité sur les ports de l’hôte (vert) |
| --- | --- | --- | --- |
| Module de contrôleur OK |ACTIVÉ |ÉTEINT |- |
| Panne de module de contrôleur |ÉTEINT |ACTIVÉ |- |
| Aucune connexion au port hôte externe |- |- |ÉTEINT |
| Connexion au port hôte externe – aucune activité |- |- |ACTIVÉ |
| Connexion au port hôte externe - activité |- |- |Clignote |
| Erreur de métadonnées du module de contrôleur |Clignote |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Lecteur de disque DEL de boîtier principal de hello et le boîtier EBOD
l’appareil StorSimple Hello possède des lecteurs de disque situés dans le boîtier principal de hello et boîtiers hello. Chaque lecteur de disque contient des voyants LED d’analyse, comme décrit dans cette section. 

Pour les lecteurs de disque hello, état hello est indiqué par un vert DEL et une DEL rouge-orange monté sur avant hello de chaque module de transport. Hello l’illustration suivante montre ces DEL.

  ![LED des lecteurs de disque][6]

Utilisez hello suivant le tableau des États de hello toodetermine de chaque lecteur de disque, qui à son tour affecte hello état des DEL du panneau frontal.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>Lecteur de disque DEL pour hello boîtiers
| État | LED d’activité OK (verte) | LED de panne (rouge-orange) | LED associées du panneau de commande |
| --- | --- | --- | --- |
| Aucun disque installé |ÉTEINT |ÉTEINT |Aucun |
| Disque installé et opérationnel |Clignotement avec l’activité |X |Aucun |
| Identité de l’appareil SES (SCSI Enclosure Services) définie |ACTIVÉ |Clignotement 1 seconde allumé/1 seconde éteint |Aucun |
| Erreur de bit de l’appareil SES définie |ACTIVÉ |ACTIVÉ |Erreur logique (rouge) |
| Panne du circuit d’alimentation |ÉTEINT |ACTIVÉ |Panne de module (rouge) |

## <a name="audible-alarms"></a>Alarmes sonores
Un appareil StorSimple intègre des alarmes sonores associées au boîtier principal de hello ainsi boîtiers hello. Une alarme sonore se trouve sur le panneau avant hello (également connu sous le nom du panneau ops hello) des deux boîtiers. alarme Hello indique quand une condition d’erreur est présente. Hello conditions suivantes est alerte hello :  

* Panne ou défaillance du ventilateur
* Tension hors plage
* Surchauffe ou température insuffisante
* Surcharge thermique
* Erreur système
* Erreur logique
* Panne d’alimentation
* Retrait d’un module d’alimentation et de refroidissement (PCM)  

Hello tableau suivant décrit hello différents États d’alarme.  

### <a name="alarm-states"></a>États d’alarme
| État d’alarme | Action | Action avec bouton muet enfoncé |
| --- | --- | --- |
| S0 |Mode normal : silencieux |Deux bips sonores |
| S1 |Mode d’erreur : 1 seconde activée/1 seconde désactivée |Passage tooS2 ou S3 (voir Remarques) |
| S2 |Mode rappel : signal sonore par intermittence |Aucun |
| S3 |Mode muet : silencieux |Aucun |
| S4 |Mode erreur/panne critique : signal sonore continu |Non disponible : le mode muet est désactivé |

> [!NOTE]
> * État d’alarme est S1, si vous n’appuyez pas sur Muet avant 2 minutes, hello état passe automatiquement tooS2 ou S3.  
> * États d’alarme S1 tooS4 retourner tooS0 après que défaillance hello est désactivée.  
> * L’alarme peut passer à l’état de panne critique S4 depuis n’importe quel autre état.  


Vous pouvez désactiver l’alarme hello en appuyant sur les bouton Muet hello du panneau ops hello. La désactivation automatique se produit après deux minutes si hello interrupteur Muet n’est pas manuellement. Lorsque l’alarme de hello est désactivée, elle continuera toosound avec tooindicate bips intermittents qu’un problème existe toujours. alarme de Hello sera silencieuse lorsque tous les problèmes de hello sont effacées.

Hello tableau suivant décrit hello différentes conditions d’alarme.

### <a name="alarm-conditions"></a>Conditions d’alarme
| État | Niveau de gravité | Alarme | LED du panneau de commande |
| --- | --- | --- | --- |
| Alerte PCM : perte d’alimentation CC d’un seul PCM |Erreur : aucune perte de redondance |S1 |Panne de module |
| Alerte PCM : perte d’alimentation CC d’un seul PCM |Erreur : perte de redondance |S1 |Panne de module |
| Défaillance du ventilateur du PCM |Erreur : perte de redondance |S1 |Panne de module |
| Le module SBB a détecté une panne de PCM |Erreur |S1 |Panne de module |
| PCM retiré |Erreur de configuration |Aucun |Panne de module |
| Erreur de configuration de boîtier |Erreur : critique |S1 |Panne de module |
| Alerte de température basse |Avertissement |S1 |Panne de module |
| Alerte de température élevée |Avertissement |S1 |Panne de module |
| Alarme de surchauffe |Erreur : critique |S1 |Panne de module |
| Défaillance du bus I2C |Erreur : perte de redondance |S1 |Panne de module |
| Erreur de communication (I2C) du panneau de commande |Erreur : critique |S1 |Panne de module |
| Erreur de contrôleur |Erreur : critique |S1 |Panne de module |
| Panne de module d’interface SBB |Erreur : critique |S1 |Panne de module |
| Panne de module d’interface SBB : aucun module opérationnel |Erreur : critique |S4 |Panne de module |
| Module d’interface SBB retiré |Avertissement |Aucun |Panne de module |
| Erreur de contrôle d’alimentation du lecteur |Avertissement : aucune perte d’alimentation du disque |S1 |Panne de module |
| Erreur de contrôle d’alimentation du lecteur |Erreur : critique ; perte d’alimentation du lecteur |S1 |Panne de module |
| Lecture retiré |Avertissement |Aucun |Panne de module |
| Alimentation insuffisante |Avertissement |Aucun |Panne de module |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [les composants matériels StorSimple et leur état](storsimple-8000-monitor-hardware-status.md).

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


