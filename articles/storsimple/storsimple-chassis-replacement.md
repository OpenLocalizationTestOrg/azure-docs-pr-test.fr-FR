---
title: "châssis aaaReplace sur l’appareil de série StorSimple 8000 | Documents Microsoft"
description: "Décrit comment tooremove et remplacer hello châssis pour votre boîtier principal de StorSimple ou d’un boîtier EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Remplacez le châssis hello sur votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment tooremove et remplacer un châssis dans un appareil de série StorSimple 8000. modèle de Hello StorSimple 8100 est un appareil à boîtier unique (un seul châssis), tandis que hello 8600 possède un double boîtier (deux châssis). Pour un modèle 8600, il existe potentiellement deux châssis qui risque d’échouer dans le dispositif de hello : hello châssis du boîtier principal hello ou châssis hello pour hello boîtiers.

Dans les deux cas, le châssis de remplacement hello fourni par Microsoft est vide. Aucun module d’alimentation et de refroidissement (PCM), module de contrôleur, disque SSD, lecteur de disque dur (HDD) ni module EBOD ne seront inclus.

> [!IMPORTANT]
> Avant de retrait et le remplacement du châssis hello, passez en revue les informations de sécurité hello dans [remplacement de composant matériel StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-chassis"></a>Retirer hello châssis
Effectuer hello suivant châssis de hello tooremove étapes sur votre appareil StorSimple.

#### <a name="tooremove-a-chassis"></a>tooremove un châssis
1. Assurez-vous que l’appareil StorSimple hello est arrêté et déconnecté de toutes les sources d’alimentation hello.
2. Supprimez tous les hello câbles réseau et SAS, le cas échéant.
3. Sortez hello de rack de hello.
4. Supprimer tous les lecteurs hello et notez les emplacements de hello à partir duquel ils sont supprimés. Pour plus d’informations, consultez [supprimer le lecteur de disque hello](storsimple-disk-drive-replacement.md#remove-the-disk-drive).
5. Sur hello boîtier EBOD (s’il s’agit de châssis hello qui a échoué), supprimez les modules de contrôleur EBOD hello. Pour plus d’informations, consultez [Retrait d’un contrôleur EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller). 
   
    Sur hello boîtier principal (s’il s’agit de châssis hello qui a échoué), supprimez les contrôleurs de hello et notez les emplacements de hello à partir duquel ils sont supprimés. Pour plus d’informations, consultez [Retrait d’un contrôleur](storsimple-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Installer hello châssis
Effectuer hello suivant châssis de hello tooinstall étapes sur votre appareil StorSimple.

#### <a name="tooinstall-a-chassis"></a>tooinstall un châssis
1. Montez le châssis hello dans un rack de hello. Pour en savoir plus, consultez la rubrique [Montage en rack de votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [Montage en rack de votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Une fois le châssis de hello est monté en rack de hello, installez les modules de contrôleur de hello Bonjour dans que même positionne qu’elles ont été précédemment installées.
3. Installation hello lecteurs Bonjour positions et emplacements qu’elles ont été précédemment installées dans.
   
   > [!NOTE]
   > Nous vous recommandons de disques SSD de hello dans les emplacements de hello d’abord installer puis installez hello HDD.
   > 
   > 
4. Avec hello appareil monté en rack de hello et hello components, connecter vos sources d’alimentation appropriées toohello appareil et activer sur l’appareil de hello. Pour en savoir plus, consultez la rubrique [Branchement des câbles de votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [Branchement des câbles de votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).

