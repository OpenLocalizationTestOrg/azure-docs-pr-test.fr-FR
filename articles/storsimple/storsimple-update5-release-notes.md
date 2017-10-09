---
title: notes de publication aaaStorSimple 8000 Series Update 5 | Documents Microsoft
description: "Décrit les nouvelles fonctionnalités de hello, des problèmes et solutions de contournement pour StorSimple 8000 Series Update 5."
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>Notes de publication de StorSimple 8000 Series Update 5

## <a name="overview"></a>Vue d'ensemble

Bonjour notes de publication suivantes décrivent les nouvelles fonctionnalités de hello et identifient les problèmes critiques en suspens hello pour StorSimple 8000 Series Update 5. Ils contiennent également une liste de mises à jour du logiciel hello StorSimple inclus dans cette version.

Mise à jour 5 peut être en cours d’exécution mise à jour 0.1 à 4 de la mise à jour de l’appareil StorSimple tooany appliqué. version de l’appareil Hello associée à 5 de la mise à jour est 6.3.9600.17845.

Consulter les informations de hello contenues dans la version hello notes avant de déployer hello mettre à jour dans votre solution StorSimple.

> [!IMPORTANT]
> * Update 5 contient les mises à jour logicielles de l’appareil, celles du microprogramme de disque, de la sécurité du système d’exploitation ainsi que d’autres mises à jour du système d’exploitation. Il prend environ 4 heures tooinstall cette mise à jour. La mise à jour du microprogramme de disque est une mise à jour perturbatrice qui entraîne une interruption de service pour votre appareil. Nous vous recommandons d’appliquer la mise à jour 5 tookeep votre appareil à jour.
> * Pour les nouvelles versions, vous ne voyiez pas les mises à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello. Revérifiez les mises à jour dans quelques jours, car celles-ci seront bientôt disponibles.

## <a name="whats-new-in-update-5"></a>Nouveautés d’Update 5

Hello améliorations clées suivantes et les correctifs de bogues ont été apportées à la mise à jour 5.

* **Utilisation de tooauthenticate d’Azure Active Directory (AAD) avec le Gestionnaire de périphériques StorSimple service** – à partir de mise à jour 5 et versions ultérieures, Azure Active Directory est tooauthenticate utilisé avec le service du Gestionnaire de périphériques StorSimple hello. mécanisme d’authentification ancien Hello sera déconseillé en décembre 2017. Tous les utilisateurs de hello doivent inclure les nouvelles URL de l’authentification hello dans leurs règles de pare-feu. Pour plus d’informations, consultez trop[URL d’authentification répertoriés dans hello configuration réseau requise pour votre appareil StorSimple](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).

    Si l’URL d’authentification hello n’est pas inclus dans les règles de pare-feu hello, les utilisateurs de hello seront affiche une alerte critique que son appareil StorSimple ne peut pas authentifier avec service de hello. Si les utilisateurs de hello voient cette alerte, ils doivent tooinclude hello nouvelle authentification URL. Pour plus d’informations, consultez trop[StorSimple mise en réseau des alertes](storsimple-8000-manage-alerts.md#networking-alerts).

* **Nouvelle version de StorSimple Snapshot Manager** : une nouvelle version de StorSimple Snapshot Manager est disponible avec Update 5. Il est recommandé que vous mettez à jour la version de toothis. Cette version est compatible avec tous les appareils StorSimple hello qui exécutent la mise à jour 3 ou version ultérieure. Pour plus d’informations, consultez trop[déployer le Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-deployment.md).


## <a name="issues-fixed-in-update-5"></a>Problèmes résolus dans Update 5

Hello tableau suivant fournit un résumé des problèmes qui ont été résolus dans la mise à jour 5.

| Non | Fonctionnalité | Problème | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- |
| 1 |Accès distant Windows PowerShell |Dans la version précédente de hello, un utilisateur reçoit une erreur lors de la tentative de tooestablish un toohello de connexion à distance StorSimple Appliance de Cloud via Windows PowerShell. La cause racine de ce problème a été identifiée et il a été résolu dans cette version. |Non |Oui |
| 2 |Modèles de bande passante |Dans la version précédente, en cas de problème avec les modèles de bande passante qui a entraîné une bande passante inférieure à quel périphérique hello a été configurée pour. Ce problème a été résolu dans cette version. |Oui |Oui |
| 3 |Basculement |Dans la version précédente, quand un appareil avec un grand nombre de volumes a basculé appareil tooanother mise à jour 4, en cours d’exécution des processus de hello échoue lors de la tentative d’enregistrements de contrôle d’accès tooapply hello. Ce problème a été résolu dans cette version. |Oui |Oui |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Problèmes connus dans Update 5 et issus des versions précédentes

Il n’existe aucun nouveau problème connu dans Update 5. Pour obtenir la liste des problèmes reportée tooUpdate 5 à partir de versions précédentes, accédez trop[notes de mise à jour 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Mises à jour du microprogramme et du contrôleur SAS (Serial-Attached SCSI) dans Update 5

Cette version contient des mises à jour du microprogramme et du pilote LSI et du contrôleur SAS. Pour plus d’informations sur comment tooinstall ces mises à jour, consultez [installer la mise à jour 5](storsimple-8000-install-update-5.md) sur votre appareil StorSimple.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>Mise à jour de StorSimple Cloud Appliance dans Update 5

Cette mise à jour ne peut pas être appliqué toohello StorSimple Appliance de Cloud (également appelé un périphérique virtuel hello). Nouveaux matériels cloud doivent toobe créé à l’aide d’image de hello 5 de la mise à jour. Pour plus d’informations sur la façon de toocreate un dispositif de StorSimple de Cloud, passez trop[déployer et gérer une application de Cloud StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="next-step"></a>Étape suivante

Découvrez comment trop[installer la mise à jour 5](storsimple-8000-install-update-5.md) sur votre appareil StorSimple.

