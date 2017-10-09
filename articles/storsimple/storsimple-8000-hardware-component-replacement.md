---
title: "remplacement de composant matériel aaaStorSimple 8000 series | Documents Microsoft"
description: "Décrit comment toosafely remplacer hello PCM, batterie, modules de contrôleur, contrôleurs EBOD, lecteurs de disque et le châssis d’un appareil StorSimple."
services: storsimple
documentationcenter: 
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
ms.custom: 
ms.openlocfilehash: 5baca8ff630a1c064cb8bf7e1024b6590f0d6b81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Remplacer un composant matériel sur votre appareil StorSimple série 8000

## <a name="overview"></a>Vue d'ensemble
didacticiels de remplacement de composant de matériel Hello décrivent les composants matériels de hello de votre Microsoft Azure StorSimple 8000 series dispositif et hello étapes nécessaire tooremove et les remplacent. Cet article décrit les icônes de sécurité hello, fournit des pointeurs toohello détaillée des didacticiels et listes hello composants sont remplaçables.

> [!IMPORTANT]
> Avant de tenter de tooremove ou remplacer n’importe quel composant StorSimple, assurez-vous que vous passez en revue les hello [conventions des icônes de sécurité](#safety-icon-conventions) et d’autres [précautions de sécurité](storsimple-safety.md).


### <a name="safety-icon-conventions"></a>Conventions des icônes de sécurité
Hello tableau suivant décrit les icônes de sécurité hello utilisés dans ces didacticiels. Accorder une attention icônes de sécurité toothese lorsque vous parcourez hello étapes tooremove et remplacez les composants de l’appareil.

| Icône | Texte | Informations supplémentaires |
|:--- |:--- |:--- |
| ![Icône Avertissement](./media/storsimple-hardware-component-replacement/Warning.png) |**DANGER !** |Signale une situation dangereuse qui, si elle n’est pas évitée, entraînera la mort ou des blessures graves. Cette signalisation ne toohello limité les situations les plus graves. |
| ![Icône Avertissement](./media/storsimple-hardware-component-replacement/Warning.png) |**AVERTISSEMENT !** |Signale une situation dangereuse qui, si elle n’est pas évitée, risque d’entraîner la mort ou des blessures graves. |
| ![Icône Attention](./media/storsimple-hardware-component-replacement/Caution.png) |**ATTENTION !** |Signale une situation dangereuse qui, si elle n’est pas évitée, risque d’entraîner des blessures légères ou moyennement graves. |
| ![Icône Information](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**INFORMATION :** |Signale des informations considérées comme importantes, mais non associées à un danger. |
| ![Icône Risque d’électrocution](./media/storsimple-hardware-component-replacement/Electric.png) |**Risque d’électrocution** |Indique un voltage élevé. |
| ![Icône Poids élevé](./media/storsimple-hardware-component-replacement/Weight.png) |**Poids élevé** | |
| ![Icône Aucune pièce remplaçable par l’utilisateur](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**Aucune pièce remplaçable par l’utilisateur** |Accès réservé au personnel formé à cet effet. |
| ![Icône Lire les instructions](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Lire toutes les instructions avant de commencer** | |
| ![Icône Risque de basculement](./media/storsimple-hardware-component-replacement/TipHazard.png) |**Risque de basculement** | |

### <a name="before-you-begin"></a>Avant de commencer
Vous devez vous familiariser avec les informations de sécurité hello sur vos icônes de périphérique et de sécurité utilisés dans ce didacticiel. Accédez trop[en toute sécurité installer et à utiliser votre appareil StorSimple](storsimple-safety.md) pour obtenir des informations complètes. Être vraiment tooreview hello [précautions de sécurité](storsimple-safety.md#handling-precautions) avant de gérer votre appareil StorSimple.

Avant de tenter de tooreplace un composant, envisagez de hello informations suivantes.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png)![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png)**AVERTISSEMENT !**

* Raccordez-vous à la terre correctement en utilisant une décharge  électrostatique ou un tapis antistatique lors de la manipulation des modules et des composants de votre appareil StorSimple.
* Ne touchez pas les circuits. Utilisez les poignées hello fournis et les guides lors de la gestion des composants de manutention.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png)![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png)**INFORMATION :**

Lorsque vous remplacez un module, **ne laissez jamais une baie vide à l’arrière de hello du boîtier de hello**. Obtenir un module vide ou remplacement avant de supprimer l’élément qui pose problème hello.

## <a name="hardware-component-replacement-procedures"></a>Procédures de remplacement des composants matériels
Votre appareil de série StorSimple 8000 se compose de plusieurs modules de plug-in Bonjour principal et/ou les boîtiers. Hello 8100 possède un boîtier principal, tandis que hello 8600 possède un double boîtier combinant un boîtier principal et un boîtier EBOD.

Hello principaux composants matériels de votre appareil sont résumées dans les tableaux suivants de hello. Cliquez sur le lien hello Bonjour **procédure de remplacement** colonne toogo toohello associés didacticiel.

| Composants | Nombre présent | Module enfichable ? | Procédure de remplacement |
|:--- |:--- |:--- |:--- |
| Châssis |1 |Non |[Remplacez le châssis hello sur votre appareil StorSimple](storsimple-8000-chassis-replacement.md) |
| Contrôleurs principaux |2 |Oui |[Remplacer un module de contrôleur sur votre appareil StorSimple](storsimple-8000-controller-replacement.md) |
| PCM (Module d’alimentation et de refroidissement) 764 W |2 |Oui |[Remplacer un module d’alimentation et de refroidissement (PCM, Power and Cooling Module) sur votre appareil StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Batterie de secours |2 |Oui |[Remplacez le module de batterie de secours hello sur votre appareil StorSimple](storsimple-8000-battery-replacement.md) |
| Lecteurs de disque |12 |Oui |[Remplacer un lecteur de disque sur votre appareil StorSimple](storsimple-8000-disk-drive-replacement.md) |

**Tableau 1** composants matériels dans le boîtier principal de hello

boîtier principal de Hello et boîtiers hello diffèrent dans les modules d’e/s. En outre, hello PCM sont de puissance différente. PCM Hello dans le boîtier principal de hello 764 W, tandis que celles de hello boîtiers sont 580 w. PCM hello Bonjour principal boîtier contiennent également un module de batterie de secours.

| Composants | Nombre présent | Module enfichable ? | Procédure de remplacement |
|:--- |:--- |:--- |:--- |
| Châssis |1 |Non |[Remplacez le châssis hello sur votre appareil StorSimple](storsimple-8000-chassis-replacement.md) |
| Contrôleurs EBOD |2 |Oui |[Remplacer un contrôleur EBOD sur votre appareil StorSimple](storsimple-8000-ebod-controller-replacement.md) |
| PCM (Module d’alimentation et de refroidissement) 580 W |2 |Oui |[Remplacer un module d’alimentation et de refroidissement (PCM, Power and Cooling Module) sur votre appareil StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Lecteurs de disque |12 |Oui |[Remplacer un lecteur de disque sur votre appareil StorSimple](storsimple-8000-disk-drive-replacement.md) |

**Tableau 2** composants matériels de hello boîtiers

modules de plug-in Hello sur l’appareil de hello sont mis en surbrillance dans hello suivant diagrammes avant et arrière. Vous pouvez utiliser ces emplacement de hello diagrammes toodetermine Hello différents modules de plug-in si un remplacement est requis. diagramme de front Hello indique hello les lecteurs de disque et des diagrammes d’arrière hello Hello EBOD boîtier et le boîtier principal de hello présente hello des modules de plug-in.

![Face avant de l’appareil avec les lecteurs de disque](./media/storsimple-hardware-component-replacement/IC741028.png)

**Figure 1** avant de l’appareil de hello

| Étiquette | Description |
|:--- |:--- |
| 0 - 11 |Lecteurs de disques (12 au total) |

Boîtier principal de hello et boîtiers hello possèdent des modules de transport de lecteur. châssis de Hello héberge douze lecteurs de disque 3,5" organisées dans un format de 3 par 4.

![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-hardware-component-replacement/IC740994.png)

**Figure 2** arrière du boîtier principal de hello

| Étiquette | Description |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Contrôleur 0 |
| 4 |Contrôleur 1 |

![Fond de panier des modules enfichables du boîtier EBOD de l’appareil](./media/storsimple-hardware-component-replacement/IC769599.png)

**Figure 3** arrière hello boîtiers

| Étiquette | Description |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Contrôleur 0 du boîtier EBOD |
| 4 |Contrôleur 1 du boîtier EBOD |

## <a name="field-replaceable-units"></a>Unités remplaçables sur site
Hello suivant unités remplaçables à chaud (FRU) est disponible pour votre appareil StorSimple :

* Châssis (y compris le panneau d’opérations intégré hello)
* Module d’alimentation et de refroidissement (PCM) en courant alternatif 764 W
* Module d’alimentation et de refroidissement (PCM) en courant alternatif 580 W
* Lecteur de disque dur avec module de support de lecteur
* Module de contrôleur
* Module de contrôleur du boîtier EBOD
* Module de batterie de secours
* Kit de rail de montage en rack

Veuillez [contactez le Support Microsoft](storsimple-8000-contact-microsoft-support.md) tooorder une de ces unités de remplacement.

## <a name="next-steps"></a>Étapes suivantes
Passez en revue tous les [les informations de sécurité](storsimple-safety.md) avant de tenter de tooreplace un composant de matériel StorSimple.

