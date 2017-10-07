---
title: "aaaInstall 2.2 de la mise à jour sur votre appareil StorSimple | Documents Microsoft"
description: "Explique comment tooinstall StorSimple 8000 Series Update 2.2 sur votre appareil de série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>Installer Update 2.2 sur votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment tooinstall 2.2 de la mise à jour sur un appareil StorSimple exécutant une version antérieure du logiciel via hello portail Azure classic et à l’aide de la méthode de correctif logiciel hello. méthode de correctif logiciel Hello est utilisé lorsqu’une passerelle est configurée sur une interface réseau autres que DATA 0 de l’appareil StorSimple hello et que vous essayez tooupdate à partir d’une version préliminaire de mise à jour du logiciel 1.

Update 2.2 inclut des mises à jour logicielles, WMI et iSCSI. Si la mise à jour depuis la version 2.1, mise à jour du logiciel de périphérique hello uniquement devez toobe appliqué. Si la mise à jour à partir d’une version 2 mise à jour préalable, vous serez également les pilotes requis tooapply LSI, Spaceport, Storport et mises à jour du microprogramme de disque. Hello logiciel des appareils, WMI, iSCSI, pilote LSI, Spaceport et Storport les correctifs sont des mises à jour sans interruption de service et peuvent être appliquées via hello portail Azure classic. mises à jour de microprogramme de disque Hello mises à jour et ne peuvent être appliqués via l’interface Windows PowerShell de hello du périphérique de hello. 

> [!IMPORTANT]
> * Un ensemble de vérifications préalables de manuels et automatiques sont effectués préalable toohello installation toodetermine hello intégrité de l’appareil en termes de matériel état et la connectivité réseau. Ces vérifications préalables sont effectuées uniquement si vous appliquez des mises à jour hello de hello portail Azure classic.
> * Nous recommandons que vous installez le logiciel de hello et mises à jour du pilote via hello portail Azure classic. Vous ne devez pas dépasser interface Windows PowerShell de toohello de l’appareil hello (tooinstall les mises à jour) en cas de vérification de mise à jour préalable passerelle hello dans le portail de hello. Selon la version de hello de que vous mettez à jour à partir, les mises à jour hello peuvent prendre 1.5-2,5 heures tooinstall. mises à jour de mode de maintenance Hello doivent être installés via l’interface Windows PowerShell de hello du périphérique de hello. Les mises à jour du mode de maintenance étant des mises à jour perturbatrices, elles entraînent un temps d’arrêt pour votre appareil.
> * Si en cours d’exécution hello facultatif StorSimple Snapshot Manager, assurez-vous que vous avez mis à niveau votre appareil hello de gestionnaire d’instantanés version tooUpdate 2.2 tooupdating préalable.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>Installer 2.2 de la mise à jour via hello portail Azure classic
Effectuer, hello suivant les étapes tooupdate votre appareil trop[2.2 de la mise à jour](storsimple-update21-release-notes.md).

> [!NOTE]
> Si vous appliquez la mise à jour 2 ou ultérieur (y compris les mises à jour 2.1), Microsoft peut être en mesure de toopull des informations de diagnostic supplémentaires à partir de l’appareil de hello. Par conséquent, lors de notre équipe d’exploitation identifie les appareils qui rencontrent des problèmes, nous meilleures informations toocollect équipés de périphériques de hello et diagnostiquer les problèmes. En acceptant la mise à jour 2 ou version ultérieure, vous nous permettez tooprovide cette prise en charge proactive.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Vérifiez que votre appareil exécute **StorSimple 8000 Series Update 2.2 (6.3.9600.17708)**. Hello **dernière date de mise à jour** doit également être modifié. 
   
   Si vous mettez à jour à partir d’un tooUpdate préalable de version 2, vous verrez également que les mises à jour de mode de Maintenance hello sont disponibles (ce message peut continuer toobe affiché pour des too24 heures après l’installation de hello mises à jour).
   
   Mises à jour du mode de maintenance sont mises à jour qui entraîne un temps d’arrêt de l’appareil et ne peuvent être appliqués via l’interface Windows PowerShell de hello de votre appareil. Dans certains cas lors de la mise à jour 1.2 sont en cours d’exécution, le microprogramme du disque est peut-être déjà à jour, auquel cas vous n’avez pas besoin tooinstall des mises à jour n’importe quel mode de maintenance.
   
   Si vous effectuez la mise à jour à partir d’Update 2, votre appareil devrait maintenant être à jour. Vous pouvez ignorer hello restant comme suit.
2. Télécharger des mises à jour de mode de maintenance hello à l’aide des étapes hello répertoriées dans [toodownload correctifs](#to-download-hotfixes) toosearch pour et télécharger KB3121899, qui installe les mises à jour du microprogramme de disque (hello autres mises à jour doivent déjà être installés à ce stade).
3. Suivez les étapes de hello répertoriées dans [installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes) mises à jour du mode maintenance tooinstall hello. 

## <a name="install-update-22-as-a-hotfix"></a>Installer Update 2.2 en tant que correctif logiciel
Utilisez cette procédure si vous ne parvenez pas à cocher de passerelle hello lors de la tentative de mises à jour de tooinstall hello hello portail Azure classic. la vérification de Hello échoue car vous disposez d’une passerelle affectée tooa non-interface réseau DATA 0 et votre appareil exécute une version de logiciel préalable tooUpdate 1.

versions logicielles Hello qui peuvent être mis à niveau à l’aide de la méthode de correctif logiciel hello sont :

* Update 0.1, 0.2, 0.3
* Update 1, 1.1, 1.2
* Update 2, 2.1 

> [!IMPORTANT]
> * Si votre appareil exécute la version de la mise en production (GA), veuillez contacter [Support technique de Microsoft](storsimple-contact-microsoft-support.md) tooassist avec hello mise à jour.
> 
> 

méthode de correctif logiciel Hello implique hello trois comme suit :

* Téléchargement de correctifs de hello de hello catalogue Microsoft Update.
* Installer et vérifier les correctifs hello mode normal.
* Installer et vérifier le correctif en mode de maintenance hello (uniquement lors de la mise à jour de logiciel de 2 avant mise à jour).

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Télécharger les mises à jour pour un appareil exécutant le logiciel Update 2.1
**Si votre appareil est en cours d’exécution 2.1 de mettre à jour**, vous devez télécharger uniquement hello périphérique mise à jour logicielle KB3179904. Installer uniquement le fichier binaire de hello commençant par 'all-hcsmdssoftwareudpate'. N’installez pas hello Cis et précédés de la mise à jour de l’agent MDS hello `all-cismdsagentupdatebundle`. Échec toodo entraînerait une erreur. Il s’agit d’une mise à jour sans interruption de service, e/s ne sont pas interrompues et les appareils hello ne disposera d’aucun temps d’arrêt.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Télécharger les mises à jour pour un appareil exécutant le logiciel Update 2
**Si votre appareil exécute la mise à jour 2**, vous devez télécharger et installer hello suivant les correctifs sur hello prescrit ordre :

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Mise à jour logicielle &#42; |Standard  <br></br>sans interruption de service |~ 45 minutes |
| 2. |KB3146621 |Package iSCSI |Standard  <br></br>sans interruption de service |~ 20 minutes |
| 3. |KB3103616 |Package WMI |Standard  <br></br>sans interruption de service |~ 12 minutes |

 &#42;  *Notez que la mise à jour logicielle se compose de deux fichiers binaires : précédés de la mise à jour logicielle de périphérique `all-hcsmdssoftwareupdate` hello Cis et précédé de l’agent de Mds `all-cismdsagentupdatebundle`. mise à jour logicielle de hello périphérique doit être installé avant hello Cis et Mds l’agent. Vous devez également redémarrer le contrôleur actif de hello via hello `Restart-HcsController` applet de commande après l’application hello éléments de configuration et mise à jour de l’agent MDS (et avant l’application hello restant mises à jour).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Télécharger les mises à jour pour un appareil exécutant une version du logiciel antérieure à Update 2
**Si votre appareil utilise une version 1.1, 1.0, 0,2 et 0,3**, vous devez télécharger et installer le pilote hello LSI et microprogramme mettre à jour en outre toohello logiciel, iSCSI et les mises à jour WMI. Cette mise à jour est déjà installée si vous exécutez Update 1.2 ou 2. 

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |Pilote LSI et microprogramme |Standard  <br></br>sans interruption de service |~ 20 minutes |

<br></br>
**Si votre appareil est en cours d’exécution versions 0,2, 0,3, 1.0, 1.1 et 1.2**, vous devez télécharger et installer hello Spaceport et correction de Storport hello. Ces correctifs sont déjà installés si vous exécutez Update 2.

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Correctif Spaceport  </br> Windows Server 2012 R2 |Standard  <br></br>sans interruption de service |~ 20 minutes |
| 6. |KB3080728 |Correctif Storport  </br> Windows Server 2012 R2 |Standard  <br></br>sans interruption de service |~ 20 minutes |

<br></br>
Vous devrez peut-être également les mises à jour de microprogramme de disque tooinstall. Vous pouvez vérifier si vous avez besoin de hello mises à jour du microprogramme de disque en exécutant hello `Get-HcsFirmwareVersion` applet de commande. Si vous exécutez ces versions du microprogramme : `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, vous n’avez pas besoin tooinstall ces mises à jour.

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Microprogramme de disque |Maintenance  <br></br>Interruption de service |~ 30 minutes |

<br></br>

> [!IMPORTANT]
> * Cette toobe de besoins procédure exécutée une seule fois tooapply 2.2 de la mise à jour. Vous pouvez utiliser les mises à jour ultérieures de hello tooapply de portail classique Azure.
> * Si la mise à jour à partir de la mise à jour 2, temps d’installation total hello est fermer too1.5 heures.
> * Avant d’utiliser cette hello tooapply de procédure mise à jour, assurez-vous que les deux contrôleurs de périphérique hello sont en ligne et tous les composants matériels de hello sont intègres.
> 
> 

Effectuer hello suivant toodownload d’étapes et installer des correctifs logiciels hello.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [Update 2.1 version](storsimple-update21-release-notes.md).

