---
title: "aaaInstall 5 de la mise à jour sur l’appareil de série StorSimple 8000 | Documents Microsoft"
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>Installer Update 5 sur votre appareil StorSimple

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel explique comment tooinstall 5 de la mise à jour sur un appareil StorSimple exécutant une version antérieure du logiciel via hello portail Azure et à l’aide de la méthode de correctif logiciel hello. méthode de correctif logiciel Hello est utilisé lorsqu’une passerelle est configurée sur une interface réseau autres que DATA 0 de l’appareil StorSimple hello et que vous essayez tooupdate à partir d’une version préliminaire de mise à jour du logiciel 1.

Update 5 comprend les mises à jour logicielles de l’appareil, celles de Storport, de Spaceport, de la sécurité du système d’exploitation et du système d’exploitation lui-même ainsi que celle du microprogramme de disque.  logiciel de périphérique Hello, Spaceport, Storport, sécurité et autres mises à jour du système d’exploitation sont mises à jour sans interruption de service. Hello sans interruption de service ou régulière des mises à jour peuvent être appliquées via hello portail Azure ou via la méthode de correctif logiciel hello. mises à jour de microprogramme de disque Hello mises à jour et sont appliquées lors de l’appareil de hello est en mode maintenance via la méthode de correctif logiciel hello à l’aide d’interface de Windows PowerShell hello du périphérique de hello.

> [!IMPORTANT]
> * Un ensemble de vérifications préalables de manuels et automatiques sont effectués préalable toohello installation toodetermine hello intégrité de l’appareil en termes de matériel état et la connectivité réseau. Ces vérifications préalables sont effectuées uniquement si vous appliquez des mises à jour hello de hello portail Azure.
> * Nous vous recommandons d’installer les logiciels hello et autres mises à jour régulières via hello portail Azure. Vous ne devez pas dépasser interface Windows PowerShell de toohello de l’appareil hello (tooinstall les mises à jour) en cas de vérification de mise à jour préalable passerelle hello dans le portail de hello. Selon la version de hello vous mettez à jour à partir de, les mises à jour hello peuvent prendre les 4 heures (ou version ultérieure) tooinstall. mises à jour de mode de maintenance Hello doivent être installés via l’interface Windows PowerShell de hello du périphérique de hello. Les mises à jour en mode de maintenance étant des mises à jour perturbatrices, elles entraînent un temps d’arrêt pour votre appareil.
> * Si en cours d’exécution hello facultatif StorSimple Snapshot Manager, assurez-vous que vous avez mis à niveau votre appareil hello de gestionnaire d’instantanés version tooUpdate 5 tooupdating préalable.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>Installer la mise à jour 5 via hello portail Azure
Effectuer, hello suivant les étapes tooupdate votre appareil trop[mise à jour 5](storsimple-update5-release-notes.md).

> [!NOTE]
> Microsoft extrait les informations de diagnostic supplémentaires à partir de l’appareil de hello. Par conséquent, lors de notre équipe d’exploitation identifie les appareils qui rencontrent des problèmes, nous meilleures informations toocollect équipés de périphériques de hello et diagnostiquer les problèmes.

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

Vérifiez que votre appareil exécute **Update 5 (6.3.9600.17845) pour la gamme d’appareils StorSimple 8000**. Hello **dernière date de mise à jour** doit être modifié.

* Vous voyez maintenant que les mises à jour de mode de Maintenance hello sont disponibles (ce message peut continuer toobe affiché pour des too24 heures après l’installation de hello mises à jour). Mises à jour du mode de maintenance sont mises à jour qui entraîne un temps d’arrêt de l’appareil et ne peuvent être appliqués via l’interface Windows PowerShell de hello de votre appareil.

* Télécharger des mises à jour de mode de maintenance hello à l’aide des étapes hello répertoriées dans [toodownload correctifs](#to-download-hotfixes) toosearch pour et télécharger KB4011837, qui installe les mises à jour du microprogramme de disque (hello autres mises à jour doivent déjà être installés à ce stade). Suivez les étapes de hello répertoriées dans [installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes) mises à jour du mode maintenance tooinstall hello.

## <a name="install-update-5-as-a-hotfix"></a>Installer Update 5 en tant que correctif logiciel


versions logicielles Hello qui peuvent être mis à niveau à l’aide de la méthode de correctif logiciel hello sont :

* Update 0.1, 0.2, 0.3
* Update 1, 1.1, 1.2
* Update 2, 2.1, 2.2
* Update 3, 3.1
* Update 4

> [!NOTE] 
> Hello recommandé tooinstall méthode que 5 de la mise à jour est via hello portail Azure. Utilisez cette procédure si vous ne parvenez pas à cocher de passerelle hello lors de la tentative de mises à jour de tooinstall hello hello portail Azure. vérification de Hello échoue lorsque vous disposez d’une passerelle affectée tooa non-interface réseau DATA 0 et que votre appareil exécute une version logicielle antérieure à la mise à jour 1.

méthode de correctif logiciel Hello implique hello trois comme suit :

1. Téléchargement de correctifs de hello de hello catalogue Microsoft Update.
2. Installer et vérifier les correctifs hello mode normal.
3. Installer et vérifier le correctif en mode de maintenance hello.

#### <a name="download-updates-for-your-device"></a>Télécharger des mises à jour pour votre appareil

Vous devez télécharger et installer hello suivant les correctifs sur hello prescrit commander et hello dossiers suggérées :

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |Installer dans le dossier|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |Mise à jour logicielle<br> Télécharger les deux fichiers _HcsSfotwareUpdate.exe_ et _CisMSDAgent.exe_ |Standard  <br></br>sans interruption de service |~ 25 minutes |FirstOrderUpdate|

Si la mise à jour à partir d’un périphérique qui exécute la mise à jour 4, vous devez uniquement les mises à jour cumulatives tooinstall hello du système d’exploitation en tant que deuxième mises à jour.

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |Installer dans le dossier|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |Package de mises à jour cumulatives de système d’exploitation <br> Télécharger la version Windows Server 2012 R2 |Standard  <br></br>sans interruption de service |- |SecondOrderUpdate|

Si l’installation à partir d’un périphérique qui exécute la mise à jour 3 ou une version antérieure, installez hello suivant en outre les mises à jour cumulatives toohello.

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation |Installer dans le dossier|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |Mises à jour du pilote et du microprogramme LSI <br> Mise à jour du microprogramme USM (version 3.38) |Standard  <br></br>sans interruption de service |~ 3 heures <br> (inclut 2A. + 2B. + 2C.)|SecondOrderUpdate|
| 2C. |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |Package de mises à jour de sécurité du système d’exploitation <br> Télécharger la version Windows Server 2012 R2 |Standard  <br></br>sans interruption de service |- |SecondOrderUpdate|
| 2D. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |Package de mises à jour du système d’exploitation <br> Télécharger la version Windows Server 2012 R2 |Standard  <br></br>sans interruption de service |- |SecondOrderUpdate|


Vous devrez peut-être également les mises à jour du microprogramme de disque tooinstall au-dessus de toutes les mises à jour de hello illustrés hello tables précédentes. Vous pouvez vérifier si vous avez besoin de hello mises à jour du microprogramme de disque en exécutant hello `Get-HcsFirmwareVersion` applet de commande. Si vous exécutez ces versions du microprogramme : `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N003`, `0107`, vous n’avez pas besoin tooinstall ces mises à jour.

| Ordre | Ko | Description | Type de mise à jour | Durée d’installation | Installer dans le dossier|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |Microprogramme de disque |Maintenance  <br></br>Interruption de service |~ 30 minutes | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Si la mise à jour à partir de la mise à jour 4, temps d’installation total hello est fermer too4 heures.
> * Avant d’utiliser cette hello tooapply de procédure mise à jour, assurez-vous que les deux contrôleurs de périphérique hello sont en ligne et tous les composants matériels de hello sont intègres.

Effectuer hello suivant toodownload d’étapes et installer des correctifs logiciels hello.

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [version de mise à jour 5](storsimple-update5-release-notes.md).

