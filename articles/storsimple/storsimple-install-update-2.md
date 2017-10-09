---
title: "aaaInstall 2 de la mise à jour sur votre appareil StorSimple | Documents Microsoft"
description: "Explique comment tooinstall StorSimple 8000 Series Update 2 sur votre appareil de série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Installer Update 2 sur votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment tooinstall mettre à jour 2 sur un appareil StorSimple exécutant une version antérieure du logiciel via hello portail Azure classic. didacticiel de Hello couvre également les étapes de hello requises pour la mise à jour hello lorsqu’une passerelle est configurée sur une interface réseau autres que DATA 0 de l’appareil StorSimple hello et que vous essayez tooupdate à partir d’une version préliminaire de mise à jour du logiciel 1.

Update 2 comprend des mises à jour logicielles de l’appareil, des mises à jour du pilote LSI et des mises à jour du microprogramme de disque. logiciel de périphérique Hello LSI les mises à jour sont mises à jour sans interruption de service et peuvent être appliquées via hello portail Azure classic. mises à jour de microprogramme de disque Hello mises à jour et ne peuvent être appliqués via l’interface Windows PowerShell de hello du périphérique de hello.

> [!IMPORTANT]
> * Vous ne pouvez pas voir 2 de la mise à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello. Revérifiez les mises à jour dans quelques jours, car celle-ci sera bientôt disponible.
> * Un ensemble de vérifications préalables de manuels et automatiques sont effectués préalable toohello installation toodetermine hello intégrité de l’appareil en termes de matériel état et la connectivité réseau. Ces vérifications préalables sont effectuées uniquement si vous appliquez des mises à jour hello de hello portail Azure classic.
> * Nous recommandons que vous installez le logiciel de hello et mises à jour du pilote via hello portail Azure classic. Vous ne devez pas dépasser interface Windows PowerShell de toohello de l’appareil hello (tooinstall les mises à jour) en cas de vérification de mise à jour préalable passerelle hello dans le portail de hello. mises à jour Hello peuvent prendre tooinstall 4-7 heures (y compris les mises à jour Windows de hello). mises à jour de mode de maintenance Hello doivent être installés via l’interface Windows PowerShell de hello du périphérique de hello. Les mises à jour du mode de maintenance étant des mises à jour perturbatrices, elles entraînent un temps d’arrêt pour votre appareil.
> * Si en cours d’exécution hello facultatif StorSimple Snapshot Manager, assurez-vous que vous avez mis à niveau votre appareil hello de gestionnaire d’instantanés version tooUpdate 2 tooupdating préalable.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Installer la mise à jour 2 via hello portail Azure classic
Effectuer, hello suivant les étapes tooupdate votre appareil trop[mise à jour 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Mise à jour 2 permet à Microsoft toopull informations de diagnostic supplémentaires à partir de l’appareil de hello. Par conséquent, lors de notre équipe d’exploitation identifie les appareils qui rencontrent des problèmes, nous meilleures informations toocollect équipés de périphériques de hello et diagnostiquer les problèmes. En acceptant la mise à jour 2, vous nous permettez tooprovide cette prise en charge proactive.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Vérifiez que votre appareil exécute **StorSimple 8000 Series Update 2 (6.3.9600.17673)**. Hello **dernière date de mise à jour** doit également être modifié. Vous verrez également que les mises à jour du mode de Maintenance sont disponibles (ce message peut continuer toobe affiché pour des too24 heures après l’installation de hello mises à jour).
   
   Mises à jour du mode de maintenance sont mises à jour qui entraîne un temps d’arrêt de l’appareil et ne peuvent être appliqués via l’interface Windows PowerShell de hello de votre appareil. Dans certains cas lors de la mise à jour 1.2 sont en cours d’exécution, le microprogramme du disque est peut-être déjà à jour, auquel cas vous n’avez pas besoin tooinstall des mises à jour n’importe quel mode de maintenance.
2. Télécharger des mises à jour de mode de maintenance hello à l’aide des étapes hello répertoriées dans [toodownload correctifs](#to-download-hotfixes) toosearch pour et télécharger KB3121899, qui installe les mises à jour du microprogramme de disque (hello autres mises à jour doivent déjà être installés à ce stade).
3. Suivez les étapes de hello répertoriées dans [installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes) mises à jour du mode maintenance tooinstall hello.

## <a name="install-update-2-as-a-hotfix"></a>Installer Update 2 en tant que correctif logiciel
Utilisez cette procédure si vous ne parvenez pas à cocher de passerelle hello lors de la tentative de mises à jour de tooinstall hello hello portail Azure classic. la vérification de Hello échoue car vous disposez d’une passerelle affectée tooa non-interface réseau DATA 0 et votre appareil exécute une version de logiciel préalable tooUpdate 1.

versions logicielles Hello qui peuvent être mis à niveau à l’aide de la méthode de correctif logiciel hello sont mises à jour 0.1, 0,2, mise à jour d’et mise à jour 0.3, mise à jour 1, 1.1 de la mise à jour et 1.2 de mise à jour. méthode de correctif logiciel Hello implique hello trois comme suit :

* Téléchargement de correctifs de hello de hello catalogue Microsoft Update.
* Installer et vérifier les correctifs hello mode normal.
* Installer et vérifier le correctif en mode de maintenance hello.

tooinstall Update 2 en tant qu’un correctif logiciel, vous devez télécharger et installer hello suivant les correctifs logiciels :

| Ordre | Ko | Description | Type de mise à jour |
| --- | --- | --- | --- |
| 1 |KB3121901 |Mise à jour logicielle |Normal |
| 2 |KB3121900 |Pilote LSI |Normal |
| 3 |KB3080728 |Correctif Storport  </br> Windows Server 2012 R2 |Normal |
| 4 |KB3090322 |Correctif Spaceport  </br> Windows Server 2012 R2 |Normal |
| 5 |KB3121899 |Microprogramme de disque |Maintenance  |

> [!IMPORTANT]
> * Si votre appareil exécute la version de la mise en production (GA), veuillez contacter [Support technique de Microsoft](storsimple-contact-microsoft-support.md) tooassist avec hello mise à jour.
> * Cette toobe de besoins procédure exécutée une seule fois tooapply 2 de la mise à jour. Vous pouvez utiliser les mises à jour ultérieures de hello tooapply de portail classique Azure.
> * Chaque installation du correctif logiciel peut prendre environ 20 minutes toocomplete. Temps total d’installation est too2 fermer heures.
> * Avant d’utiliser cette hello tooapply de procédure mise à jour, assurez-vous que les deux contrôleurs sont en ligne et tous les composants matériels de hello sont intègres.
> 
> 

Effectuer hello suivant les étapes tooapply cette mise à jour en tant que correctif.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [version 2 de la mise à jour](storsimple-update2-release-notes.md).

