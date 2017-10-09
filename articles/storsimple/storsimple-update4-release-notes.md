---
title: "notes de mise à jour de la série 4 aaaStorSimple 8000 | Documents Microsoft"
description: "Décrit les nouvelles fonctionnalités de hello, des problèmes et solutions de contournement pour StorSimple 8000 Series Update 4."
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
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>Notes de publication de StorSimple série 8000 Update 4

## <a name="overview"></a>Vue d'ensemble

Bonjour notes de publication suivantes décrivent les nouvelles fonctionnalités de hello et identifient les problèmes critiques en suspens hello pour StorSimple 8000 Series Update 4. Ils contiennent également une liste de mises à jour du logiciel hello StorSimple inclus dans cette version. 

Mise à jour 4 peut être en cours d’exécution mise en production (GA) ou mise à jour 0.1 à 3.1 de mise à jour de l’appareil StorSimple tooany appliqué. version de l’appareil Hello liée à la mise à jour 4 est 6.3.9600.17820.

Veuillez consulter les informations de hello contenues dans la version de hello notes avant de déployer hello mettre à jour dans votre solution StorSimple.

> [!IMPORTANT]
> * Update 4 comprend le logiciel de l’appareil, le microprogramme USM, le pilote et le microprogramme LSI, le microprogramme du disque, Storport et Spaceport, la mise à jour de sécurité et d’autres mises à jour du système d’exploitation. Il prend environ 4 heures tooinstall cette mise à jour. La mise à jour du microprogramme de disque est une mise à jour perturbatrice qui entraîne une interruption de service pour votre appareil. Nous vous recommandons d’appliquer la mise à jour 4 tookeep votre appareil à jour. 
> * Pour les nouvelles versions, vous ne voyiez pas les mises à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello. Revérifiez les mises à jour dans quelques jours, car elles seront bientôt disponibles.

## <a name="whats-new-in-update-4"></a>Nouveautés d’Update 4

Hello améliorations clées suivantes et les correctifs de bogues ont été apportées à la mise à jour 4.

* **Plus intelligente automatisée des algorithmes de récupération de l’espace** – dans la mise à jour 4, hello algorithmes de récupération automatique d’espace sont récupération de l’espace tooadjust étendu hello cycles selon hello attendu récupéré l’espace disponible dans le cloud de hello. 

* **Améliorations des performances pour les volumes attachés localement** – mise à jour 4 a amélioré les performances de hello de volumes attachés localement dans les scénarios qui ont l’ingestion de données élevé (taille des données comparables toovolume).

* **Restauration Heatmap** - Bonjour précédemment mises en production, après une récupération d’urgence (DR), les données de salutation a été restaurées à partir du cloud hello basée sur des modèles d’accès hello entraîne un ralentissement des performances. 

    Une nouvelle fonctionnalité est implémentée dans la mise à jour 4 que pistes fréquence d’accès aux données toocreate un heatmap lorsque hello périphérique est tooDR préalable d’utilisation (utilisés le plus de segments de données ont chaleur élevée, tandis que les moins utilisés par segments ont moins de chaleur). Après la récupération d’urgence, StorSimple utilise hello heatmap tooautomatically restauration ou de réalimente les données hello du cloud de hello. 

    Toutes les restaurations hello sont désormais heatmap en fonction des restaurations. Pour plus d’informations sur comment heatmap tooquery et annuler en fonction des travaux de restauration et la réactivation, consultez trop[Windows PowerShell pour la référence d’applet de commande StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

* **Outil de diagnostic de StorSimple** : de mise à jour 4, un outil est en cours de diagnostic StorSimple publié tooallow de diagnostic simple et dépannage des problèmes liés à toosystem réseau et des performances matérielles d’intégrité de composant. Cet outil est exécuté via hello Windows PowerShell pour StorSimple. Pour plus d’informations, consultez trop[dépannage à l’aide d’outil de diagnostic de StorSimple](storsimple-8000-diagnostics.md).

* **Outil de Migration de StorSimple basée sur l’interface utilisateur** -toothis préalables la version finale, la migration des données de 7000 de 5000 série requis hello utilisateurs tooexecute une partie du flux de travail de migration hello à l’aide d’interface d’Azure PowerShell hello. Dans cette version, une simple à utiliser en fonction de l’interface utilisateur de la Migration de StorSimple outil devient disponible pour une prise en charge toofacilitate hello même flux de travail de migration. Cet outil permettrait également de consolidation hello de compartiments de récupération. 

* **Modifications liées à la norme FIPS** - cette version et les versions ultérieures, FIPS est activé par défaut sur tous les appareils de série StorSimple 8000 de hello pour les deux hello Microsoft Azure Government et comptes de cloud public Azure.

* **Mettre à jour des modifications** : dans cette version, les bogues de tooupdate connexes échecs ont été résolus.

* **Alerte de défaillance de disque** -une nouvelle alerte qui avertit l’utilisateur hello de défaillances imminentes de disque est ajoutée dans cette version. Si vous rencontrez cette alerte, contactez le Support technique de Microsoft tooship un disque de remplacement. Pour plus d’informations, consultez trop[alertes matérielles sur votre appareil StorSimple](storsimple-manage-alerts.md#hardware-alerts).

* **Modifications de remplacement de contrôleur** -une applet de commande qui permet d’état de hello tooquery hello utilisateur du processus de remplacement de contrôleur hello est ajoutée dans cette version. Pour plus d’informations, consultez toohello [état de remplacement du contrôleur applet de commande tooquery](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Problèmes résolus dans Update 4

Hello tableau suivant fournit un résumé des problèmes qui ont été résolus dans la mise à jour 4.    

| Non | Fonctionnalité | Problème | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- |
| 1 |Basculement |Bonjour version précédente, après le basculement hello, il y a un problème lié toocleanup observé sur le site client hello. Ce problème a été résolu dans cette version. |Oui |Oui |
| 2 |Volumes épinglés localement  |Version précédente de hello, il y avait une création de volume toorelated problème pour les volumes attachés localement qui entraînerait des échecs de création de volume. La cause racine de ce problème a été identifiée et il a été résolu dans cette version. |Oui |Non |
| 3 |Package de prise en charge |Dans la version précédente, comportaient package tooSupport connexes de problèmes qui entraînerait une exception System.OutOfMemory ou d’autres erreurs entraîne l’échec de la création de package de prise en charge. Ces bogues ont été résolus dans cette version. |Oui |Oui |
| 4 |Surveillance |Dans la version précédente, il d’un problème lié graphiques toomonitoring pour les volumes attachés localement où la consommation était affichée dans EB. Ce bogue a été résolu dans cette version. |Oui |Oui |
| 5 |Migration |Dans la version précédente, comportaient plusieurs fiabilité toohello connexes de problèmes de migration à partir de périphériques too8000 séries 5000-7000. Ces problèmes ont été résolus dans cette version. |Oui |Oui |
| 6 |Mettre à jour |Dans les versions précédentes, s’il existe un échec de la mise à jour, les contrôleurs hello va passer en mode de récupération et par conséquent, utilisateur de hello Impossible de poursuivre la mise à jour de hello et devez toocontact Support technique de Microsoft. <br> Ce comportement a été modifié dans cette version. Si l’utilisateur de hello a un échec de la mise à jour une fois que les deux contrôleurs hello sont en cours d’exécution hello même version (mettre à jour 4), hello contrôleurs n’entrez pas en mode de récupération. Si l’utilisateur de hello rencontre cette erreur, nous recommandons qu’ils attendez un peu et recommencez la mise à jour de hello. nouvelle tentative de Hello peut réussir. Si les tentatives de hello échoue, ils doivent contacter le Support Microsoft. |Oui |Oui |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Problèmes connus dans Update 4 depuis les versions précédentes

Il n’existe aucun nouveau problème connu dans Update 4. Pour obtenir la liste des problèmes reportée tooUpdate 4 à partir de versions précédentes, accédez trop[notes de mise à jour 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Mises à jour du microprogramme et du contrôleur Serial-Attached SCSI (SAS) dans Update 4

Cette version contient des mises à jour du microprogramme et du pilote LSI et du contrôleur SAS. Pour plus d’informations sur comment tooinstall ces mises à jour, consultez [installer la mise à jour 4](storsimple-install-update-4.md) sur votre appareil StorSimple.

## <a name="virtual-device-updates-in-update-4"></a>Mises à jour des appareils virtuels dans Update 4

Cette mise à jour ne peut pas être appliqué toohello StorSimple Appliance de Cloud (également appelé un périphérique virtuel hello). Nouveaux périphériques virtuels devez toobe créé. 

## <a name="next-step"></a>Étape suivante

Découvrez comment trop[installer la mise à jour 4](storsimple-install-update-4.md) sur votre appareil StorSimple.

