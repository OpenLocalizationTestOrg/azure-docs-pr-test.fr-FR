---
title: "aaaInstall 1.2 de mise à jour sur votre appareil StorSimple | Documents Microsoft"
description: "Explique comment tooinstall StorSimple 8000 Series Update 1.2 sur votre appareil de série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>Installer Update 1.2 sur votre appareil StorSimple série 8000
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment tooinstall mettre à jour 1.2 sur un appareil StorSimple qui s’exécute une version de logiciel préalable tooUpdate 1. didacticiel de Hello couvre également les étapes supplémentaires hello requis pour la mise à jour hello lorsqu’une passerelle est configurée sur une interface réseau autres que DATA 0 de l’appareil StorSimple hello.

Update 1.2 comprend des mises à jour logicielles de l’appareil, des mises à jour du pilote LSI et des mises à jour du microprogramme de disque. Bonjour logiciels et mises à jour du pilote LSI sont mises à jour sans interruption de service et peuvent être appliquées via hello portail Azure classic. mises à jour de microprogramme de disque Hello mises à jour et ne peuvent être appliqués via l’interface Windows PowerShell de hello du périphérique de hello.

Selon la version en cours d’exécution sur votre appareil, vous pouvez déterminer si Update 1.2 sera appliqué. Vous pouvez vérifier la version du logiciel hello de votre appareil en accédant toohello **coup de œil rapide** section de votre appareil **tableau de bord**.

</br>

| Si vous exécutez la version logicielle… | Que se passe-t-il dans le portail de hello ? |
| --- | --- |
| Version commerciale - GA |Si vous exécutez la version commerciale (GA), n’appliquez pas cette mise à jour. Veuillez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) tooupdate votre appareil. |
| Update 0.1 |Le portail applique Update 1.2. |
| Update 0.2 |Le portail applique Update 1.2. |
| Update 0.3 |Le portail applique Update 1.2. |
| Update 1 |Cette mise à jour ne sera pas disponible. |
| Update 1.1 |Cette mise à jour ne sera pas disponible. |

</br>

> [!IMPORTANT]
> * Vous ne pouvez pas voir 1.2 de mise à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello. Revérifiez les mises à jour dans quelques jours, car celle-ci sera bientôt disponible.
> * Cette mise à jour comprend un ensemble de l’intégrité du manuel et automatique des vérifications préalables toodetermine hello périphérique en termes de matériel état et la connectivité réseau. Ces vérifications préalables sont effectuées uniquement si vous appliquez des mises à jour hello de hello portail Azure classic.
> * Nous recommandons que vous installez le logiciel de hello et mises à jour du pilote via hello portail Azure classic. Vous ne devez pas dépasser interface Windows PowerShell de toohello de l’appareil hello (tooinstall les mises à jour) en cas de vérification de mise à jour préalable passerelle hello dans le portail de hello. mises à jour Hello peuvent prendre tooinstall 5 à 10 heures (y compris les mises à jour Windows de hello). mises à jour de mode de maintenance Hello doivent être installés via l’interface Windows PowerShell de hello du périphérique de hello. Les mises à jour du mode de maintenance étant des mises à jour perturbatrices, elles entraînent un temps d’arrêt pour votre appareil.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>Installer 1.2 de mise à jour via hello portail Azure classic
Effectuer, hello suivant les étapes tooupdate votre appareil trop[mise à jour 1.2](storsimple-update1-release-notes.md). Utilisez cette procédure uniquement si vous disposez d’une passerelle configurée sur l’interface réseau DATA 0 de votre appareil.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Vérifiez que votre appareil exécute **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**. Hello **dernière date de mise à jour** doit également être modifié. Vous verrez également que les mises à jour du mode de Maintenance sont disponibles (ce message peut continuer toobe affiché pour des too24 heures après l’installation de hello mises à jour).
   
   Mises à jour du mode de maintenance sont mises à jour qui entraîne un temps d’arrêt de l’appareil et ne peuvent être appliqués via l’interface Windows PowerShell de hello de votre appareil.
   
   ![Page Maintenance](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Page Maintenance")
2. Télécharger des mises à jour de mode de maintenance hello à l’aide des étapes hello répertoriées dans [toodownload correctifs](#to-download-hotfixes) toosearch pour et télécharger KB3063416, qui installe les mises à jour du microprogramme de disque (hello autres mises à jour doivent déjà être installés à ce stade).
3. Suivez les étapes de hello répertoriées dans [installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes) mises à jour du mode maintenance tooinstall hello.
4. Dans l’hello portail Azure classic, accédez toohello **Maintenance** page et en bas de hello de page de hello, cliquez sur **d’analyse des mises à jour** toocheck pour toutes les mises à jour Windows puis cliquez sur **installer les mises à jour** . Vous avez terminé une fois toutes les Hello mises à jour sont correctement installés.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Installation d’Update 1.2 sur un appareil présentant une passerelle configurée pour une interface réseau différente de DATA 0.
Vous devez utiliser cette procédure uniquement si vous ne parvenez pas à cocher de passerelle hello lors de la tentative de mises à jour de tooinstall hello hello portail Azure classic. la vérification de Hello échoue car vous disposez d’une passerelle affectée tooa non-interface réseau DATA 0 et votre appareil exécute une version de logiciel préalable tooUpdate 1. Si votre appareil ne dispose pas d’une passerelle sur une non-interface réseau DATA 0, vous pouvez mettre à jour votre appareil directement à partir de hello portail Azure classic. Consultez [installation mise à jour 1.2 via hello portail Azure classic](#install-update-1.2-via-the-azure-classic-portal).

versions logicielles Hello pouvant être mis à niveau à l’aide de cette méthode sont mise à jour 0.1, mise à jour 0,2 et mise à jour 0.3.

> [!IMPORTANT]
> * Si votre appareil exécute la version de la mise en production (GA), veuillez contacter [Support technique de Microsoft](storsimple-contact-microsoft-support.md) tooassist avec hello mise à jour.
> * Cette toobe de besoins procédure exécutée une seule fois tooapply 1.2 de mise à jour. Vous pouvez utiliser les mises à jour ultérieures de hello tooapply de portail classique Azure.
> 
> 

Si votre appareil est en cours d’exécution avant mise à jour des 1 logiciels et a une passerelle définie pour une interface réseau autres que DATA 0, vous pouvez appliquer 1.2 de mise à jour de hello deux façons suivantes :

* **Option 1**: télécharger la mise à jour hello et l’appliquer à l’aide de hello `Start-HcsHotfix` applet de commande à partir de l’interface Windows PowerShell de hello du périphérique de hello. Il s’agit de méthode recommandée de hello. **Si votre appareil exécute la mise à jour 1.0 ou 1.1 de la mise à jour, n’utilisez pas cette méthode de tooapply 1.2 de mise à jour.**
* **Option 2**: configuration de la passerelle Remove hello et installation Bonjour mettre à jour directement à partir de hello portail Azure classic.

Instructions détaillées pour chacun d’eux sont fournies dans les sections suivantes de hello.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>Option 1 : Utiliser Windows PowerShell pour StorSimple tooapply 1.2 de mise à jour en tant que correctif
Vous devez utiliser cette procédure uniquement si vous exécutez la mise à jour 0.1, 0,2, 0,3 et si votre vérification de la passerelle a échoué lors de la tentative de mises à jour tooinstall hello portail Azure classic. Si vous exécutez un logiciel de mise en production (GA), veuillez [Support technique de Microsoft](storsimple-contact-microsoft-support.md) tooupdate votre appareil.

tooinstall 1.2 de mise à jour en tant qu’un correctif logiciel, vous devez télécharger et installer hello suivant les correctifs logiciels :

| Ordre | Ko | Description | Type de mise à jour |
| --- | --- | --- | --- |
| 1 |KB3063418 |Mise à jour logicielle |Normal |
| 2 |KB3043005 |Mise à jour du contrôleur SAS LSI |Normal |
| 3 |KB3063416 |Microprogramme de disque |Maintenance  |

Avant d’utiliser cette hello tooapply de procédure mise à jour, assurez-vous que :

* Les deux contrôleurs d’appareil sont en ligne.

Effectuer hello suivant les étapes tooapply 1.2 de mise à jour. **mises à jour Hello peut prendre environ 2 heures toocomplete (environ 30 minutes pour les logiciels, 30 minutes pour pilote, 45 minutes pour le microprogramme du disque).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>Option 2 : Utiliser hello tooapply portail classique Azure 1.2 de mise à jour après la suppression de configuration de la passerelle hello
Cette procédure s’applique uniquement les appareils tooStorSimple qui exécutent une version de logiciel préalable tooUpdate 1 et ont une passerelle définie sur une interface réseau autres que DATA 0. Vous aurez besoin de mise à jour tooclear hello passerelle paramètre tooapplying préalable hello.

mise à jour Hello peut prendre quelques heures toocomplete. Si vos ordinateurs hôtes se trouvent dans des sous-réseaux différents, suppression de la configuration de passerelle hello sur des interfaces hello iSCSI peut entraîner un temps d’arrêt. Nous vous recommandons de configurer DATA 0 pour les temps d’arrêt du hello tooreduce le trafic iSCSI.

Effectuer hello suivant l’interface de réseau étapes toodisable hello avec la passerelle de hello, puis appliquez la mise à jour de hello.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [version de mise à jour 1.2](storsimple-update1-release-notes.md).

