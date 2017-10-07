---
title: "aaaInstall 4 de la mise à jour sur l’appareil de série StorSimple 8000 | Documents Microsoft"
description: "Explique comment tooinstall StorSimple 8000 Series Update 4 sur votre appareil de série StorSimple 8000."
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 3507edbde5e6e43b6c450bfea19494d47b5a5ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Installer Update 4 sur votre appareil StorSimple

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel explique comment tooinstall 4 de la mise à jour sur un appareil StorSimple exécutant une version antérieure du logiciel via hello portail Azure et à l’aide de la méthode de correctif logiciel hello. méthode de correctif logiciel Hello est utilisé lorsqu’une passerelle est configurée sur une interface réseau autres que DATA 0 de l’appareil StorSimple hello et que vous essayez tooupdate à partir d’une version préliminaire de mise à jour du logiciel 1.

Update 4 comprend les mises à jour du logiciel de l’appareil, du microprogramme USM, du pilote et du microprogramme LSI, de Storport, de Spaceport, de sécurité du système d’exploitation et beaucoup d’autres mises à jour du système d’exploitation.  logiciel de périphérique Hello, le microprogramme USM, Spaceport, Storport et autres mises à jour du système d’exploitation sont mises à jour sans interruption de service. Hello sans interruption de service ou régulière des mises à jour peuvent être appliquées via hello portail Azure ou via la méthode de correctif logiciel hello. mises à jour de microprogramme de disque Hello mises à jour et ne peuvent être appliqués via la méthode de correctif logiciel hello à l’aide d’interface de Windows PowerShell hello du périphérique de hello.

> [!IMPORTANT]
> * Un ensemble de vérifications préalables de manuels et automatiques sont effectués préalable toohello installation toodetermine hello intégrité de l’appareil en termes de matériel état et la connectivité réseau. Ces vérifications préalables sont effectuées uniquement si vous appliquez des mises à jour hello de hello portail Azure.
> * Nous vous recommandons d’installer les logiciels hello et autres mises à jour régulières via hello portail Azure. Vous ne devez pas dépasser interface Windows PowerShell de toohello de l’appareil hello (tooinstall les mises à jour) en cas de vérification de mise à jour préalable passerelle hello dans le portail de hello. Selon la version de hello vous mettez à jour à partir de, les mises à jour hello peuvent prendre les 4 heures (ou version ultérieure) tooinstall. mises à jour de mode de maintenance Hello doivent également être installés via l’interface Windows PowerShell de hello du périphérique de hello. Les mises à jour du mode de maintenance étant des mises à jour perturbatrices, elles entraînent un temps d’arrêt pour votre appareil.
> * Si en cours d’exécution hello facultatif StorSimple Snapshot Manager, assurez-vous que vous avez mis à niveau votre appareil hello de gestionnaire d’instantanés version tooUpdate 4 tooupdating préalable.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-portal"></a>Installer la mise à jour 4 via hello portail Azure
Effectuer, hello suivant les étapes tooupdate votre appareil trop[mise à jour 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Microsoft extrait les informations de diagnostic supplémentaires à partir de l’appareil de hello. Par conséquent, lors de notre équipe d’exploitation identifie les appareils qui rencontrent des problèmes, nous meilleures informations toocollect équipés de périphériques de hello et diagnostiquer les problèmes. 

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update4-via-portal.md)]

Vérifiez que votre appareil exécute **StorSimple 8000 Series Update 4 (6.3.9600.17820)**. Hello **dernière date de mise à jour** doit également être modifié.

* Vous voyez maintenant que les mises à jour de mode de Maintenance hello sont disponibles (ce message peut continuer toobe affiché pour des too24 heures après l’installation de hello mises à jour). Mises à jour du mode de maintenance sont mises à jour qui entraîne un temps d’arrêt de l’appareil et ne peuvent être appliqués via l’interface Windows PowerShell de hello de votre appareil.

* Télécharger des mises à jour de mode de maintenance hello à l’aide des étapes hello répertoriées dans [toodownload correctifs](#to-download-hotfixes) toosearch pour et télécharger KB4011837, qui installe les mises à jour du microprogramme de disque (hello autres mises à jour doivent déjà être installés à ce stade). Suivez les étapes de hello répertoriées dans [installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes) mises à jour du mode maintenance tooinstall hello.

## <a name="install-update-4-as-a-hotfix"></a>Installer Update 4 en tant que correctif logiciel
Hello recommandé tooinstall méthode que Hello portail Azure est mise à jour 4.

Utilisez cette procédure si vous ne parvenez pas à cocher de passerelle hello lors de la tentative de mises à jour de tooinstall hello hello portail Azure. la vérification de Hello échoue car vous disposez d’une passerelle affectée tooa non-interface réseau DATA 0 et votre appareil exécute une version de logiciel préalable tooUpdate 1.

versions logicielles Hello qui peuvent être mis à niveau à l’aide de la méthode de correctif logiciel hello sont :

* Update 0.1, 0.2, 0.3
* Update 1, 1.1, 1.2
* Update 2, 2.1, 2.2
* Update 3, 3.1


méthode de correctif logiciel Hello implique hello trois comme suit :

1. Téléchargement de correctifs de hello de hello catalogue Microsoft Update.
2. Installer et vérifier les correctifs hello mode normal.
3. Installer et vérifier le correctif en mode de maintenance hello.

#### <a name="download-updates-for-your-device"></a>Télécharger des mises à jour pour votre appareil

Vous devez télécharger et installer hello suivant les correctifs sur hello prescrit commander et hello dossiers suggérées :

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |Installer dans le dossier|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 |Mise à jour logicielle |Standard  <br></br>sans interruption de service |~ 25 minutes |FirstOrderUpdate|
| 2A. |KB4011841 <br> KB4011842 |Mises à jour du pilote et du microprogramme LSI <br> Mise à jour du microprogramme USM (version 3.38) |Standard  <br></br>sans interruption de service |~ 3 heures <br> (inclut 2A. + 2B. + 2C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3197873 <br> KB3192392, KB3153704 <br> KB3174644, KB3139914  |Package de mises à jour de sécurité du système d’exploitation <br> Télécharger Windows Server 2012 R2 |Standard  <br></br>sans interruption de service |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |Package de mises à jour du système d’exploitation <br> Télécharger Windows Server 2012 R2 |Standard  <br></br>sans interruption de service |- |SecondOrderUpdate|

Vous devrez peut-être également les mises à jour du microprogramme de disque tooinstall au-dessus de toutes les mises à jour de hello illustrés hello tables précédentes. Vous pouvez vérifier si vous avez besoin de hello mises à jour du microprogramme de disque en exécutant hello `Get-HcsFirmwareVersion` applet de commande. Si vous exécutez ces versions du microprogramme : `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, vous n’avez pas besoin tooinstall ces mises à jour.

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation | Installer dans le dossier|
| --- | --- | --- | --- | --- | --- |
| 3. |KB3121899 |Microprogramme de disque |Maintenance  <br></br>Interruption de service |~ 30 minutes | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Cette toobe de besoins procédure exécutée une seule fois tooapply mise à jour 4. Vous pouvez utiliser les mises à jour ultérieures de hello tooapply portail Azure.
> * Si la mise à jour à partir de la mise à jour 3 ou 3.1, moment de l’installation de total hello est fermer too4 heures.
> * Avant d’utiliser cette hello tooapply de procédure mise à jour, assurez-vous que les deux contrôleurs de périphérique hello sont en ligne et tous les composants matériels de hello sont intègres.

Effectuer hello suivant toodownload d’étapes et installer des correctifs logiciels hello.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [version de mise à jour 4](storsimple-update4-release-notes.md).

