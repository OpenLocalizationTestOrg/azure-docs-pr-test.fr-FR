---
title: "notes de 0,5 virtuel mise à jour du tableau aaaStorSimple | Documents Microsoft"
description: "Décrit les ouvrir critiques mettre à jour les problèmes et solutions pour l’exécution de StorSimple Virtual Array hello 0,5."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>Notes de publication de StorSimple Virtual Array Update 0.5

## <a name="overview"></a>Vue d'ensemble

Bonjour notes de publication suivantes identifient les problèmes critiques en suspens hello et hello problèmes résolus pour les mises à jour de Microsoft Azure StorSimple Virtual Array.

notes de publication Hello sont mis à jour, et que les problèmes critiques nécessitant une solution de contournement sont découverts, ils sont ajoutés. Avant de déployer votre StorSimple Virtual Array, lisez attentivement les informations hello contenues dans les notes hello.

Mise à jour 0,5 correspond la version du logiciel toohello **10.0.10290.0**.

> [!NOTE]
> Les mises à jour entraînent des perturbations et redémarrent votre appareil. Si les e/s sont en cours, appareil de hello implique un temps d’arrêt. Pour obtenir des instructions détaillées sur la façon dont tooapply hello mise à jour, accédez trop[installation mise à jour 0,5](storsimple-virtual-array-install-update-05.md).


## <a name="whats-new-in-hello-update-05"></a>Nouveautés de hello mise à jour 0,5
Update 0.5 est essentiellement une version de correctif de bogue. améliorations Hello et des correctifs de bogues sont comme suit :

- **Améliorations de la résilience de sauvegarde** -cette version comporte des correctifs qui améliorent la sauvegarde de hello. Bonjour les versions antérieures, les sauvegardes ont été retentées uniquement de certaines exceptions. Cette version nouvelle tentative toutes les exceptions de sauvegarde hello et rend hello sauvegardes plus fiable.

- **Mises à jour pour la surveillance de l’utilisation de stockage** -depuis le 30 juin 2017, hello de surveillance de l’utilisation de stockage pour la série d’appareils virtuels StorSimple vont être supprimées. Cela s’applique toohello graphiques sur tous les tableaux virtuels hello mise à jour en cours d’exécution inférieur ou égal à 0,4 de surveillance. Cette mise à jour contient des modifications de hello requises pour vous toocontinue hello utilisation de l’utilisation du stockage analyse Bonjour portail Azure. Installez cette mise à jour critique avant le 30 juin 2017 toocontinue à l’aide de la fonctionnalité d’analyse de hello.


## <a name="issues-fixed-in-hello-update-05"></a>Problèmes résolus dans hello mise à jour 0,5

Hello tableau suivant fournit un résumé des problèmes résolus dans cette version.

| Non. | Fonctionnalité | Problème |
| --- | --- | --- |
| 1 |Résilience de sauvegarde| Bonjour les versions antérieures, les sauvegardes ont été retentées uniquement de certaines exceptions. Cette version contient un correctif toomake des sauvegardes plus résilient en tentant d’exécuter toutes les exceptions de sauvegarde hello.|
| 2 |Surveillance| surveillance de l’utilisation Hello stockage pour la série d’appareils virtuels StorSimple sera déconseillée en commençant le 30 juin 2017. Cette action a un impact sur hello graphiques sur le service de gestionnaire de périphériques StorSimple hello en cours d’exécution sur les réseaux virtuels StorSimple de surveillance (modèle 1200). Cette version comporte des mises à jour qui permettent l’utilisation de hello hello utilisateur toocontinue de surveillance de l’utilisation de stockage sur les tableaux de virtuel hello au-delà du 30 juin 2017.|
| 3 |Serveur de fichiers| Bonjour les versions antérieures, un utilisateur peut copier par erreur tableau virtuel toohello de fichiers chiffrés. Cette version contient un correctif qui ne permet pas d’une copie du tableau de toovirtual les fichiers chiffrés. Si votre appareil a toohello préalable des fichiers chiffrés existant à mettre à jour, sauvegardes de continue toofail jusqu'à ce que tous les fichiers hello chiffré sont supprimés hello système. |


## <a name="known-issues-in-hello-update-05"></a>Problèmes connus dans hello mise à jour 0,5

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
| **8.** |Capacité utilisée pour les partages |Vous pouvez voir partager la consommation lorsque aucune donnée sur le partage de hello. Cette consommation est, car la capacité hello utilisé pour les partages inclut des métadonnées. | |
| **9.** |Récupération d'urgence |Vous ne pouvez effectuer la récupération d’urgence hello d’un toohello de serveur de fichier même domaine que celui de l’appareil source de hello. Appareil de cible de tooa de récupération d’urgence dans un autre domaine n’est pas pris en charge dans cette version. |Ceci est implémenté dans une version ultérieure. Pour plus d’informations, consultez trop[basculement et récupération d’urgence de votre tableau virtuel StorSimple](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |périphériques virtuels StorSimple de Hello ne peut pas être gérés via hello Azure PowerShell dans cette version. |Toute la gestion de périphériques virtuels de hello hello doit être effectuée via hello Azure portal et hello interface utilisateur web locale. |
| **11.** |Modification de mot de passe |Hello console de l’appareil virtuel tableau accepte uniquement les entrées dans la norme en-us clavier format. | |
| **12.** |CHAP |Il est impossible de supprimer les informations d’identification CHAP une fois qu’elles ont été créées. En outre, si vous modifiez les informations d’identification de hello CHAP, vous devez volumes hors connexion de tootake hello et puis les mettez en ligne pour modifier un effet de tootake hello. |Ce problème est résolu dans une version ultérieure. |
| **13.** |Serveur iSCSI |Hello utilisé le stockage affiché pour un volume iSCSI peut être différent dans le service du Gestionnaire de périphériques StorSimple hello et hôte iSCSI de hello. |ordinateur hôte iSCSI de Hello possède la vue de système de fichiers de hello.<br></br>Appareil de Hello voit blocs hello allouées lorsque le volume de hello était à la taille maximale de hello. |
| **14.** |Serveur de fichiers |Si un fichier dans un dossier a un autre flux de données (ADS) associé, hello annonces n’est pas sauvegardé ou restauré via la récupération d’urgence, de clonage et de récupération au niveau de l’élément. | |
| **15.** |Serveur de fichiers |Les liens symboliques ne sont pas pris en charge. | |
| **16.** |Serveur de fichiers |Fichiers protégés par Windows EFS (ENCRYPTING file) lorsque copiée ou stockées sur hello résultats StorSimple Virtual Array du serveur de fichiers dans une configuration non prise en charge.  | |

## <a name="next-step"></a>Étape suivante
[Installation d’Update 0.5](storsimple-virtual-array-install-update-05.md) sur StorSimple Virtual Array.

## <a name="references"></a>Références
Vous recherchez une note de version antérieure ? Accédez à :

* [Notes de publication de StorSimple Virtual Array Update 0.4](storsimple-virtual-array-update-04-release-notes.md)
* [Notes de publication de StorSimple Virtual Array Update 0.3](storsimple-ova-update-03-release-notes.md)
* [Notes de publication de StorSimple Virtual Array Update 0.1 et 0.2](storsimple-ova-update-01-release-notes.md)
* [Notes de publication de StorSimple Virtual Array General Availability](storsimple-ova-pp-release-notes.md)

