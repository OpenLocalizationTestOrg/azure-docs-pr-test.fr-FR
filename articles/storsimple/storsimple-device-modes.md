---
title: "mode de l’appareil StorSimple hello aaaChange | Documents Microsoft"
description: "Décrit les modes du périphérique StorSimple hello et explique comment toouse Windows PowerShell pour StorSimple toochange hello mode de l’appareil."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>Modifier le mode d’appareil hello sur votre appareil StorSimple
Cet article fournit une brève description de hello différents modes dans lesquels votre appareil StorSimple peut fonctionner. Votre appareil StorSimple peut fonctionner dans trois modes : Normal, Maintenance et Récupération. 

À la fin de cet article, vous :

* Quels sont les modes du périphérique StorSimple hello
* Comment toofigure quel mode hello appareil StorSimple est en
* Comment toochange du mode de toomaintenance normal et *inversement*

Hello au-dessus des tâches de gestion ne peut être effectuée via l’interface Windows PowerShell de hello de votre appareil StorSimple.

## <a name="about-storsimple-device-modes"></a>À propos des modes de l’appareil StorSimple
Votre appareil StorSimple peut fonctionner en mode Normal, Maintenance ou Récupération. Chacun de ces modes est brièvement décrit ci-dessous.

### <a name="normal-mode"></a>Mode Normal
Cela est défini comme mode de fonctionnement normal hello pour un appareil StorSimple entièrement configuré. Par défaut, votre appareil doit être en mode Normal.

### <a name="maintenance-mode"></a>Mode Maintenance
Parfois hello appareil StorSimple peut-être toobe placé en mode maintenance. Ce mode vous permet de tooperform maintenance sur l’appareil de hello et installer les mises à jour, telles que celles liées toodisk microprogramme.

Vous pouvez placer le système de hello en mode de maintenance uniquement via hello Windows PowerShell pour StorSimple. Dans ce mode, toutes les demandes d’E/S sont suspendues. Services tels que de mémoire vive non volatile (NVRAM) ou le service de cluster de hello sont également arrêtés. Les deux contrôleurs hello sont redémarrés lorsque vous entrez ou quittez ce mode. Lorsque vous quittez le mode de maintenance hello, tous les services hello reprendront et doivent être sains. Cela peut prendre quelques minutes.

> [!NOTE]
> **Le mode Maintenance est uniquement pris en charge sur un appareil en état de fonctionnement. Il n’est pas pris en charge sur un périphérique dans lequel une ou les deux contrôleurs de hello ne fonctionnent pas.**
> </br>
> 
> 

### <a name="recovery-mode"></a>Mode Récupération
Le mode Récupération peut être décrit comme un « mode sans échec avec prise en charge du réseau Windows ». En mode de récupération s’engage équipe de Support technique de Microsoft hello et leur permet tooperform diagnostics sur le système de hello. Hello principal en mode de récupération vise les journaux système tooretrieve hello.

Si votre système passe en mode Récupération, vous devez contacter le support technique Microsoft pour les étapes suivantes. Pour plus d’informations, consultez trop[contactez le Support technique Microsoft](storsimple-contact-microsoft-support.md).

> [!NOTE]
> **Impossible de placer les appareils hello en mode de récupération. Si l’appareil de hello est en mauvais état, en mode de récupération tente de périphérique de hello tooget dans un état dans lequel le personnel de Support technique de Microsoft peut l’examiner.**
> 
> 

## <a name="determine-storsimple-device-mode"></a>Détermination du mode de l’appareil StorSimple
#### <a name="toodetermine-hello-current-device-mode"></a>mode de périphérique en cours toodetermine hello
1. Ouvrez une session sur la console série du périphérique toohello en suivant les étapes de hello dans [console série du périphérique toohello tooconnect utilisez PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Examinez le message de bannière hello dans le menu de console série hello du périphérique de hello. Ce message indique explicitement si l’appareil de hello est en mode de maintenance ou de récupération. Si le message de type hello ne contient pas d’informations spécifiques concernant le mode du système toohello, appareil de hello est en mode normal.

## <a name="change-hello-storsimple-device-mode"></a>Modifier le mode de l’appareil StorSimple hello
Vous pouvez placer l’appareil StorSimple hello dans la maintenance de maintenance mode (mode normal) tooperform ou installer des mises à jour du mode de maintenance. Effectuer hello suivant les procédures tooenter ou sortie en mode maintenance.

> [!IMPORTANT]
> Avant de passer en mode maintenance, vérifiez que les deux contrôleurs d’appareil sont intègres en accédant à hello **état du matériel** sur hello **Maintenance** page Bonjour portail Azure classic. Si un ou les deux contrôleurs de hello ne sont pas sains, contactez le Support Microsoft pour les étapes suivantes de hello. Pour plus d’informations, consultez trop[contactez le Support technique Microsoft](storsimple-contact-microsoft-support.md).
> 
> 

#### <a name="tooenter-maintenance-mode"></a>mode de maintenance tooenter
1. Ouvrez une session sur la console série du périphérique toohello en suivant les étapes de hello dans [console série du périphérique toohello tooconnect utilisez PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**. Lorsque vous y êtes invité, fournissez hello **mot de passe administrateur**. mot de passe Hello : `Password1`.
3. À l’invite de commandes hello, tapez 
   
    `Enter-HcsMaintenanceMode`
4. Vous verrez un message d’avertissement indiquant que le mode maintenance s’interrompre toutes les demandes d’e/s serveur hello connexion toohello portail Azure classic et vous serez invité à confirmer l’opération. Type **Y** tooenter le mode maintenance.
5. Les deux contrôleurs redémarrent. Lorsque le redémarrage de hello est terminée, un autre message s’affiche, indiquant que ce périphérique hello est en mode maintenance.

#### <a name="tooexit-maintenance-mode"></a>mode de maintenance tooexit
1. Ouvrez une session sur la console série du périphérique toohello. Vérifiez à partir du message de bannière hello que votre appareil est en mode maintenance.
2. À l’invite de commandes hello, tapez :
   
    `Exit-HcsMaintenanceMode`
3. Un message d’avertissement et un message de confirmation s’affichent. Type **Y** tooexit le mode maintenance.
4. Les deux contrôleurs redémarrent. Lorsque le redémarrage de hello est terminée, un autre message s’affiche, indiquant que ce périphérique hello est en mode normal.

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[appliquer les mises à jour de mode normal et de maintenance](storsimple-update-device.md) sur votre appareil StorSimple.

