---
title: aaaUpdate votre appareil StorSimple | Documents Microsoft
description: "Explique comment toouse hello StorSimple mettre à jour tooinstall fonctionnalité régulière et des correctifs et mises à jour du mode de maintenance."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Mettre à jour votre appareil StorSimple 8000 Series
## <a name="overview"></a>Vue d'ensemble
Hello StorSimple mises à jour les fonctionnalités permettent tooeasily jour votre appareil StorSimple. Selon le type de mise à jour de hello, vous pouvez appliquer les appareil de toohello de mises à jour via le portail Azure classic de hello ou via l’interface Windows PowerShell de hello. Ce didacticiel décrit les types de mise à jour hello et comment tooinstall d'entre eux.

Vous pouvez appliquer deux types de mises à jour d’appareil : 

* Mises à jour ordinaires (ou en mode Normal)
* Mises à jour en mode Maintenance

Vous pouvez installer les mises à jour régulières via hello portail Azure classic ou Windows PowerShell ; Toutefois, vous devez utiliser des mises à jour du mode Maintenance tooinstall Windows PowerShell. 

Chaque type de mise à jour est décrit séparément, ci-dessous.

### <a name="regular-updates"></a>Mises à jour ordinaires
Mises à jour régulières sont mises à jour sans interruption de service qui peuvent être installés lors de l’appareil de hello est en mode Normal. Ces mises à jour sont appliquées via le contrôleur de l’appareil tooeach du site Web Microsoft Update hello. 

> [!IMPORTANT]
> Un basculement de contrôleur peut se produire pendant le processus de mise à jour hello. Mais cela n’aura aucune incidence sur la disponibilité ou le fonctionnement du système.
> 
> 

* Pour plus d’informations sur comment tooinstall mises à jour régulières hello via le portail Azure classic, consultez [installer les mises à jour régulières via hello portail Azure classic](#install-regular-updates-via-the-azure-classic-portal).
* Vous pouvez également installer les mises à jour ordinaires via Windows PowerShell pour StorSimple Pour des informations détaillées, consultez la page [Installer les mises à jour ordinaires via Windows PowerShell pour StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Mises à jour en mode Maintenance
Les mises à jour en mode Maintenance provoquent une interruption du service. Il s’agit, par exemple, des mises à niveau du microprogramme du disque. Ces mises à jour nécessitent hello appareil toobe est placé en mode Maintenance. Pour plus d’informations, consultez l’[Étape 2 : Passage en mode Maintenance](#step2). Vous ne pouvez pas utiliser les mises à jour du mode Maintenance tooinstall de portail classique Azure hello. Vous devez utiliser Windows PowerShell pour StorSimple. 

Pour plus d’informations sur comment le mode de Maintenance tooinstall met à jour, consultez [mises à jour du mode de Maintenance d’installer via Windows PowerShell pour StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Mode de gestion des mises à jour doivent être appliquée séparément tooeach contrôleur. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Installer les mises à jour régulières via hello portail Azure classic
Vous pouvez utiliser l’appareil StorSimple tooyour hello tooapply de portail classique Azure mises à jour.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Installer les mises à jour ordinaires via Windows PowerShell pour StorSimple
Ou bien, vous pouvez utiliser Windows PowerShell pour StorSimple tooapply les mises à jour régulières (mode Normal).

> [!IMPORTANT]
> Vous pouvez installer les mises à jour normales à l’aide de Windows PowerShell pour StorSimple, nous vous recommandons vivement d’installer les mises à jour régulières via hello portail Azure classic. À partir de mise à jour 1, vérifications préalables sera effectuée tooinstalling préalable des mises à jour à partir du portail de hello. Ces vérifications préalables permettent de prévenir les échecs et de garantir une expérience avec moins de problèmes. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Installer les mises à jour en mode Maintenance via Windows PowerShell pour StorSimple
Vous utilisez Windows PowerShell pour l’appareil StorSimple de tooyour StorSimple tooapply Maintenance mode mises à jour. Dans ce mode, toutes les demandes d’E/S sont suspendues. Services tels que de mémoire vive non volatile (NVRAM) ou le service de cluster de hello sont également arrêtés. Les deux contrôleurs sont redémarrés lorsque vous entrez dans ce mode ou que vous le quittez. Lorsque vous quittez ce mode, tous les services hello reprendront et doivent être sains. (Cela peut prendre quelques minutes.)

Si vous avez besoin de mises à jour de mode de Maintenance tooapply, vous recevrez une alerte via hello portail classique Azure que vous disposez des mises à jour qui doivent être installés. Cette alerte inclut des instructions sur l’utilisation de Windows PowerShell pour les mises à jour de StorSimple tooinstall hello. Une fois que vous mettez à jour votre appareil, utilisez hello même mode de procédure toochange hello périphérique tooRegular. Pour obtenir des instructions détaillées, consultez l’ [Étape 4 : Sortie du mode Maintenance](#step4).

> [!IMPORTANT]
> * Avant de passer en mode Maintenance, vérifiez que les deux contrôleurs d’appareil sont intègres en vérifiant hello **état du matériel** sur hello **Maintenance** page Bonjour portail Azure classic. Si le contrôleur de hello n’est pas intègre, contactez le Support Microsoft pour les étapes suivantes de hello. Pour plus d’informations, consultez tooContact Support technique de Microsoft. 
> * Lorsque vous êtes en mode Maintenance, vous devez tooapply hello tout d’abord les mises à jour sur un contrôleur et puis sur hello autre contrôleur.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Étape 1 : Connecter la console série de toohello<a name="step1">
Tout d’abord, utilisez une application tel que PuTTY tooaccess hello console série. Hello procédure suivante explique comment console série du toohello toouse tooconnect PuTTY.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Étape 2 : Passage en mode Maintenance <a name="step2">
Une fois que vous vous connectez toohello console, déterminez s’il existe des mises à jour tooinstall et entrez tooinstall de mode de Maintenance les.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Étape 3 : Installation des mises à jour <a name="step3">
Ensuite, installez les mises à jour.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Étape 4 : Sortie du mode Maintenance <a name="step4">
Pour finir, quittez le mode Maintenance.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Installer les correctifs logiciels via Windows PowerShell pour StorSimple
Contrairement aux mises à jour pour Microsoft Azure StorSimple, les correctifs logiciels sont installés à partir d’un dossier partagé. Comme pour les mises à jour, il existe deux types de correctifs : 

* Correctifs logiciels ordinaires 
* Correctifs logiciels en mode Maintenance  

Hello procédures suivantes expliquent comment toouse Windows PowerShell pour tooinstall StorSimple régulière et des correctifs en mode Maintenance.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>Que se passe-t-il tooupdates si vous effectuez une fabrique de réinitialisation du périphérique de hello ?
Si un appareil est toofactory de réinitialiser les paramètres, toutes les mises à jour de hello sont perdues. Une fois l’appareil réinitialisé de hello est inscrit et configuré, vous devez toomanually installer les mises à jour via hello portail Azure classic et/ou de Windows PowerShell pour StorSimple. Pour plus d’informations sur les paramètres d’usine, consultez [rétablir les paramètres par défaut de hello appareil toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [à l’aide Windows PowerShell pour StorSimple tooadminister votre appareil StorSimple](storsimple-windows-powershell-administration.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

