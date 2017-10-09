---
title: "notes de publication de mises à jour de tableau virtuel aaaStorSimple | Documents Microsoft"
description: "Décrit les ouvrir critiques et les solutions pour l’exécution de StorSimple Virtual Array hello mise à jour 0.3."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>Notes de publication de StorSimple Virtual Array Update 0.3
## <a name="overview"></a>Vue d'ensemble
Bonjour notes de publication suivantes identifient les problèmes critiques en suspens hello et hello problèmes résolus pour les mises à jour de Microsoft Azure StorSimple Virtual Array.

notes de publication Hello sont mis à jour, et que les problèmes critiques nécessitant une solution de contournement sont découverts, ils sont ajoutés. Avant de déployer votre StorSimple Virtual Array, lisez attentivement les informations hello contenues dans les notes hello.

Mise à jour 0.3 correspond la version du logiciel toohello **10.0.10288.0**.

> [!NOTE]
> Les mises à jour entraînent des perturbations et redémarrent votre appareil. Si les e/s sont en cours, appareil de hello implique un temps d’arrêt.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>Nouveautés de hello mise à jour 0.3
Update 0.3 est essentiellement une version de correctif de bogue. Dans cette version, ce qui entraîne des échecs de sauvegarde dans la version précédente de hello de plusieurs bogues ont été traités.

## <a name="issues-fixed-in-hello-update-03"></a>Problèmes résolus dans hello mise à jour 0.3
Hello tableau suivant fournit un résumé des problèmes résolus dans cette version.

| Non. | Fonctionnalité | Problème |
| --- | --- | --- |
| 1 |Sauvegardes |Un problème a été détecté en hello version antérieure, où les sauvegardes hello échouerait toocomplete pour un partage de fichiers. Si ce problème s’est produite, sauvegarde hello échoue et une alerte critique a été déclenchée sur hello StorSimple Manager toonotify hello utilisateur. Ce problème ne se pas affecter les données hello sur des partages de hello ou accéder aux données de toohello. cause première Hello a été identifié et résolu dans cette version. <br></br> correctif de Hello ne s’applique pas rétroactivement tooshares qui mesurent déjà ce problème. Les clients qui vous rencontrez ce problème doivent tout d’abord appliquer la mise à jour 0.3, puis contactez le Support technique de Microsoft tooperform un problème de hello toofix sauvegarde complète du système. Au lieu de contacter le Support Microsoft, clients peuvent également restaurer tooa nouveau partage à partir d’une sauvegarde saine pour les partages hello affectée. |
| 2 |iSCSI |Un problème a été détecté en hello version antérieure, où les volumes hello disparaît lors de la copie du volume de données tooa hello StorSimple Virtual Array. Ce problème a été résolu dans cette version. <br></br> correctifs de Hello prennent effet uniquement sur nouvellement créé des volumes. correctifs de Hello ne s’appliquent pas rétroactivement toovolumes qui mesurent déjà ce problème. Il est conseillé de clients toobring hello affectée volumes en ligne via hello portail Azure classic, effectuer une sauvegarde pour ces volumes et puis restaurer ces volumes toonew de volumes. |

## <a name="known-issues-in-hello-update-03"></a>Problèmes connus dans hello mise à jour 0.3
Bonjour tableau suivant fournit un résumé des problèmes connus de hello StorSimple Virtual Array et inclut des problèmes hello indication mise en production à partir de versions précédentes de hello. 

| Non. | Fonctionnalité | Problème | Solution de contournement/commentaires |
| --- | --- | --- | --- |
| **1.** |Mises à jour |les périphériques virtuels Hello créés dans la version préliminaire de hello ne peut pas être la version disponibilité générale de mise à jour tooa pris en charge. |Ces périphériques virtuels doivent être basculés pour hello version disponibilité générale à l’aide d’un flux de travail de récupération d’urgence. |
| **2.** |Disque de données configuré |Une fois, vous avez configuré un disque de données d’une certaine taille spécifiée et créé hello correspondant un appareil virtuel StorSimple, vous ne devez pas développer ou réduire disque de données hello. Tentative de toodo entraîne une perte de toutes les données hello dans les niveaux de hello local de l’appareil de hello. | |
| **3.** |Stratégie de groupe |Quand un appareil est joint au domaine, appliquer une stratégie de groupe peut nuire opération de périphérique hello. |Assurez-vous que votre tableau virtuel est dans sa propre unité d’organisation (UO) pour Active Directory et aucun objet de stratégie de groupe (GPO) n’est appliqué tooit. |
| **4.** |Interface utilisateur web locale |Si les fonctionnalités de sécurité améliorées sont activées dans Internet Explorer (IE ESC), certaines pages de l’interface utilisateur web locale, comme Dépannage ou Maintenance, peuvent ne pas fonctionner correctement. Les boutons sur ces pages peuvent également ne pas fonctionner. |Désactivez les fonctionnalités de sécurité améliorées d'Internet Explorer. |
| **5.** |Interface utilisateur web locale |Sur un ordinateur virtuel Hyper-V, hello interfaces réseau dans web hello l’interface utilisateur sont affichés sous la forme d’interfaces de 10 Gbits/s. |Ce comportement est le reflet de Hyper-V. Hyper-V affiche toujours 10 Gbits/s pour les cartes de réseau virtuel. |
| **6.** |Partages ou volumes à plusieurs niveaux |Plage d’octets pour les applications qui fonctionnent avec hello StorSimple volumes hiérarchisés de verrouillage n’est pas pris en charge. Si le verrouillage de la plage d’octets est activé, la hiérarchisation StorSimple ne fonctionne pas. |Mesures recommandées :  <br></br>Désactivez le verrouillage de plage d'octets dans la logique de votre application.<br></br>Choisissez tooput les données pour cette application dans les volumes attachés localement par opposition tootiered volumes.<br></br>*Avertissement*: lorsqu’à l’aide locale épinglée de volumes et verrouillage de plage d’octets est activé, le volume de hello attaché localement peut être en ligne avant même que la restauration hello est terminée. Dans ce cas, si une restauration est en cours, puis vous devez attendre hello restauration toocomplete. |
| **7.** |Partages à plusieurs niveaux |L'utilisation de fichiers volumineux peut entraîner montée en charge de niveau lente. |Lorsque vous travaillez avec des fichiers volumineux, nous vous recommandons de que ce fichier le plus volumineux hello est inférieur à 3 % de la taille du partage hello. |
| **8.** |Capacité utilisée pour les partages |Vous pouvez voir partager la consommation lorsque aucune donnée sur le partage de hello. Il s’agit, car la capacité hello utilisé pour les partages inclut des métadonnées. | |
| **9.** |Récupération d'urgence |Vous ne pouvez effectuer la récupération d’urgence hello d’un toohello de serveur de fichier même domaine que celui de l’appareil source de hello. Appareil de cible de tooa de récupération d’urgence dans un autre domaine n’est pas pris en charge dans cette version. |Ceci est implémenté dans une version ultérieure. |
| **10.** |Azure PowerShell |périphériques virtuels StorSimple de Hello ne peut pas être gérés via hello Azure PowerShell dans cette version. |Toute la gestion de périphériques virtuels de hello hello doit être effectuée via hello portail Azure classic et web locale de hello l’interface utilisateur. |
| **11.** |Modification de mot de passe |console de l’appareil virtuel tableau Hello accepte uniquement les entrées au format de clavier en-US. | |
| **12.** |CHAP |Il est impossible de supprimer les informations d’identification CHAP une fois qu’elles ont été créées. En outre, si vous modifiez les informations d’identification de hello CHAP, vous devez volumes hors connexion de tootake hello et puis les mettez en ligne pour modifier un effet de tootake hello. |Ce problème est résolu dans une version ultérieure. |
| **13.** |Serveur iSCSI |Hello utilisé le stockage affiché pour un volume iSCSI peut être différent dans le service StorSimple Manager hello et hôte iSCSI de hello. |ordinateur hôte iSCSI de Hello possède la vue de système de fichiers de hello.<br></br>Appareil de Hello voit blocs hello allouées lorsque le volume de hello était à la taille maximale de hello. |
| **14.** |Serveur de fichiers |Si un fichier dans un dossier a un autre flux de données (ADS) associé, hello annonces n’est pas sauvegardé ou restauré via la récupération d’urgence, de clonage et de récupération au niveau de l’élément. | |

## <a name="next-step"></a>Étape suivante
[Installation d’Update 0.3](storsimple-ova-install-update-01.md) sur StorSimple Virtual Array.

## <a name="references"></a>Références
Vous recherchez une note de version antérieure ? Accédez à : 

* [Notes de publication de StorSimple Virtual Array Update 0.1 et 0.2](storsimple-ova-update-01-release-notes.md)
* [Notes de publication de StorSimple Virtual Array General Availability](storsimple-ova-pp-release-notes.md)

